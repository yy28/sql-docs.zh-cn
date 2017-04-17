---
title: "第 5 课：部署和使用模型（数据科学端到端演练）| Microsoft Docs"
ms.custom: 
ms.date: 11/22/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: f28a7aac-6d08-4781-ad28-b48d18cc16a0
caps.latest.revision: 17
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 753420824012402c14921811745693e2f1910442
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-5-deploy-and-use-the-model-data-science-end-to-end-walkthrough"></a>第 5 课：部署和使用模型（数据科学端到端演练）
在本课程中，你将通过在存储过程中包装持久化模型，在生产环境中使用 R 模型。 随后可以通过 R 或支持 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的任何应用程序编程语言（如 C#、Java、Python 等）调用存储过程，以使用模型对新的观测值进行预测。  
  
可以通过两种不同方式来调用模型进行计分：  
  
-   通过**批处理计分模式** 可以基于来自 SELECT 查询的输入创建多个预测。  
  
-   通过**单个计分模式** 可以一次创建一个预测，具体方法是将用于单独情况的一组特征值传递给存储过程，而存储过程会返回单个预测或其他值作为结果。  
  
你将学习如何使用单个计分和批处理计分方法创建预测。  
  
## <a name="batch-scoring"></a>批处理计分  
为方便起见，可以使用最初在第 1 课中运行 PowerShell 脚本时创建的存储过程。 此存储过程执行以下操作：  
  
-   以 SQL 查询的形式获取一组输入数据    
-   调用在上一课中保存的已定型逻辑回归模型    
-   预测司机获得小费的概率  
  
### <a name="use-the-stored-procedure-predicttipbatchmode"></a>使用存储过程 PredictTipBatchMode

1. 花点时间看一下用于定义存储过程 *PredictTipBatchMode*的脚本。 它说明了如何使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]实施模型的几个方面。  
  
    ```tsql  
    CREATE PROCEDURE [dbo].[PredictTipBatchMode]   
    @input nvarchar(max)  
    AS  
    BEGIN  
  
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  FROM nyc_taxi_models);  
      EXEC sp_execute_external_script @language = N'R',  
         @script = N'  
           mod <- unserialize(as.raw(model));  
           print(summary(mod))  
           OutputDataSet<-rxPredict(modelObject = mod, 
               data = InputDataSet, 
               outData = NULL, 
               predVarNames = "Score", type = "response", 
               writeModelVars = FALSE, overwrite = TRUE);  
           str(OutputDataSet)  
           print(OutputDataSet)',  
      @input_data_1 = @input,  
      @params = N'@model varbinary(max)',  
      @model = @lmodel2  
      WITH RESULT SETS ((Score float));  
    END    
    ```  

    + 请注意调用存储的模型的 SELECT 语句。 你可以使用类型为 **varbinary(max)**的列在 SQL 表中存储任何已定型的模型。 在此代码中，模型从表中进行检索，存储在 SQL 变量 _@lmodel2_ 中，并作为参数 *mod* 传递给系统存储过程 [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。
    + 用于计分的输入数据会作为字符串传递给存储过程。  
  
        若要为此特定模型定义输入数据，请创建返回有效数据的查询。 因为数据是从数据库进行检索，所以数据存储在名为 InputDataSet 的数据帧中。 此数据帧中的所有行都用于批处理计分。
        + InputDataSet 是 [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 的输入数据的默认名称；可以在需要时定义其他变量名称。
        + 为了生成分数，存储过程会从 **RevoScaleR** 库调用 *rxPredict* 函数。
    + 存储过程的返回值 Score 是司机获得小费的预测概率。  
  
2.  （可选）可轻松将某种类型的筛选器应用于返回值，将返回值分类到“有小费”或“无小费”组中。  例如，概率小于 0.5 意味着可能无小费。  
  
3.  以批处理模式调用存储过程：  
  
    ```R  
    input = "N' 
      SELECT TOP 10 
          a.passenger_count AS passenger_count,   
          a.trip_time_in_secs AS trip_time_in_secs,  
          a.trip_distance AS trip_distance,  
          a.dropoff_datetime AS dropoff_datetime,    
          dbo.fnCalculateDistance(
            pickup_latitude, 
            pickup_longitude, 
            dropoff_latitude,
            dropoff_longitude) AS direct_distance   
      FROM  
      
      (SELECT medallion, hack_license, pickup_datetime,   
      passenger_count,trip_time_in_secs,trip_distance,    
      dropoff_datetime, pickup_latitude, pickup_longitude,   
      dropoff_latitude, dropoff_longitude from nyctaxi_sample)a  
      
      LEFT OUTER JOIN  
 
      ( SELECT medallion, hack_license, pickup_datetime 
        FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b  

      ON a.medallion=b.medallion 
        AND a.hack_license=b.hack_license 
        AND a.pickup_datetime=b.pickup_datetime  

      WHERE b.medallion is null  
    '"  
    q<-paste("EXEC PredictTipBatchMode @inquery = ", input, sep="")  
    sqlQuery (conn, q)  
  
    ```  
  
## <a name="single-row-scoring"></a>单行计分  

你可能要将特征作为参数传递给存储过程，而不是使用查询将输入值传递给保存的 R 模型。  

### <a name="use-the-stored-procedure-predicttipsinglemode"></a>使用存储过程 PredictTipSingleMode
1.  花点时间看一下以下用于存储过程 *PredictTipSingleMode*的代码，它应已在你的数据库中创建。  
  
    ```tsql  
    CREATE PROCEDURE [dbo].[PredictTipSingleMode] @passenger_count int = 0,  
    @trip_distance float = 0,  
    @trip_time_in_secs int = 0,  
    @pickup_latitude float = 0,  
    @pickup_longitude float = 0,  
    @dropoff_latitude float = 0,  
    @dropoff_longitude float = 0  
    AS  
    BEGIN  
      DECLARE @inquery nvarchar(max) = N'  
        SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, 
            @trip_distance,  
            @trip_time_in_secs,  
            @pickup_latitude,  
            @pickup_longitude,  
            @dropoff_latitude,  
            @dropoff_longitude)  
        '  
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);  

      EXEC sp_execute_external_script @language = N'R',  @script = N'  
            mod <- unserialize(as.raw(model));  
            print(summary(mod))  
            OutputDataSet<-rxPredict(
                     modelObject = mod, 
                     data = InputDataSet, 
                     outData = NULL,   
                     predVarNames = "Score", 
                     type = "response", 
                     writeModelVars = FALSE, 
                     overwrite = TRUE);  
            str(OutputDataSet)  
            print(OutputDataSet)  
            ',  
      @input_data_1 = @inquery,  
      @params = N'@model varbinary(max),
                @passenger_count int,
                @trip_distance float,
                @trip_time_in_secs int ,  
                @pickup_latitude float ,
                @pickup_longitude float ,
                @dropoff_latitude float ,
                @dropoff_longitude float',  
                @model = @lmodel2,  
                @passenger_count =@passenger_count ,  
                @trip_distance=@trip_distance,  
                @trip_time_in_secs=@trip_time_in_secs,    
                @pickup_latitude=@pickup_latitude,  
                @pickup_longitude=@pickup_longitude,  
                @dropoff_latitude=@dropoff_latitude,  
                @dropoff_longitude=@dropoff_longitude  
      WITH RESULT SETS ((Score float));  
    END    
    ```  
  
    此存储过程采用特征值作为输入（如乘客计数和行程距离），使用存储的 R 模型对这些特征进行计分，然后输出分数。  
  
### <a name="call-the-stored-procedure-and-pass-parameters"></a>调用存储过程并传递参数

1. 在 SQL Server Management Studio 中，可使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC** 调用存储过程，并将其传递给所需的输入。 的脚本。  
    ```tsql  
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303   
    ```  
  
    此处传递的值分别用于变量 _passenger_count_、 _trip_distance_、 _trip_time_in_secs_、 _pickup_latitude_、 _pickup_longitude_、 _dropoff_latitude_和 _dropoff_longitude_。  
  
2.  若要从 R 代码运行此相同的调用，只需定义包含整个存储过程调用的 R 变量。 
  
    ```R  
    q = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 "  
    ```  
  
    此处传递的值分别用于变量 _passenger_count_、 _trip_distance_、 _trip_time_in_secs_、 _pickup_latitude_、 _pickup_longitude_、 _dropoff_latitude_和 _dropoff_longitude_。  
  
### <a name="generate-scores"></a>生成评分

1. 调用 *RODBC* 包的 **sqlQuery** 函数，并传递连接字符串和包含存储过程调用的字符串变量。  
  
    ```R  
    # predict with stored procedure in single mode  
    sqlQuery (conn, q)   
    ```  
  
    有关 **RODBC**的详细信息，请参阅 [http://www.inside-r.org/packages/cran/RODBC/docs/sqlQuery](http://www.inside-r.org/packages/cran/RODBC/docs/sqlQuery)。  
  
## <a name="conclusion"></a>结语  
现在，你已学习了如何处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据并将已定型 R 模型保存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，那么基于此数据集创建一些其他模型对于你而言应该比较容易。 例如，你可能会尝试创建类似以下这些的模型：  
  
-   预测小费金额的回归模型    
-   预测小费是较多、中等还是较少的多类分类模型。  

我们还建议你查看一些其他示例和资源： 
+ [数据科学方案和解决方案模板](../../advanced-analytics/r-services/data-science-scenarios-and-solution-templates.md)
+ [数据库内高级分析](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)
+ [Microsoft R - Diving into Data Analysis](https://msdn.microsoft.com/microsoft-r/data-analysis-in-microsoft-r)
+ [Additional Resources](https://msdn.microsoft.com/microsoft-r/microsoft-r-more-resources)
## <a name="previous-lesson"></a>前一课  
[第 4 课：生成并保存模型（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="see-also"></a>另请参阅  
[SQL Server R Services 教程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  


