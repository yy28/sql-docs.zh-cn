---
title: "第 4 课：生成并保存模型（数据科学端到端演练）| Microsoft Docs"
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
ms.assetid: 69b374c1-2042-4861-8f8b-204a6297c0db
caps.latest.revision: 20
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 423b7a7a0aadd7a22e301a43721aa6d1a15802cd
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough"></a>第 4 课：生成并保存模型（数据科学端到端演练）
在本课程中，你将学习如何生成机器学习模型并将该模型保存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中。  
  
## <a name="creating-a-classification-model"></a>创建分类模型  
你将生成的模型是二元分类器，可以预测出租车司机是否有可能在某次搭乘中获得小费。 你将使用在上一课中创建的数据源 `featureDataSource,` ，通过逻辑回归来定型小费分类器。  
  
以下是将在模型中使用的功能：  
  
-   passenger_count  
  
-   trip_distance  
  
-   trip_time_in_secs  
  
-   direct_distance  

### <a name="create-the-model-using-rxlogit"></a>使用 rxLogit 创建模型  
1.  调用包括在 *RevoScaleR* 包中的 **rxLogit** 函数，创建逻辑回归模型。  
  
    ```R  
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource))    
    ```  
    + 生成模型的调用封装在 system.time 函数中。 这样，你便可获得生成模型所需的时间。
    
2.  生成模型后，你需要使用 `summary` 函数检查模型，并查看系数。  
  
    ```  
    summary(logitObj)  
    ```  

     *结果*

     *Logistic Regression Results for: tipped ~ passenger_count + trip_distance + trip_time_in_secs +*  
     *direct_distance*  
     *Data: featureDataSource (RxSqlServerData Data Source)*  
     *Dependent variable(s): tipped*  
     *Total independent variables: 5*   
     *Number of valid observations: 17068*  
     *Number of missing observations: 0*   
     *-2\*LogLikelihood: 23540.0602 (Residual deviance on 17063 degrees of freedom)*  
     *Coefficients:*  
     *Estimate Std.Error z value Pr(>|z|)*   
     *(Intercept)       -2.509e-03  3.223e-02  -0.078  0.93793*   
     *passenger_count   -5.753e-02  1.088e-02  -5.289 1.23e-07 \*\*\**  
     *trip_distance     -3.896e-02  1.466e-02  -2.658  0.00786 \*\**   
     *trip_time_in_secs  2.115e-04  4.336e-05   4.878 1.07e-06 \*\*\**  
     *direct_distance    6.156e-02  2.076e-02   2.966  0.00302 \*\**   
     *---*  
     *Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’0.1 ‘ ’ 1*  
     *Condition number of final variance-covariance matrix: 48.3933*   
     *Number of iterations: 4*  
  
### <a name="use-the-logistic-regression-model-for-scoring"></a>使用逻辑回归模型进行计分  
既然已生成模型，可以用其来预测出租车司机是否有可能在某次搭乘中获得小费。  
  
1.  首先，定义要用于存储评分结果的数据对象  
  
    ```R  
    scoredOutput <- RxSqlServerData(  
      connectionString = connStr,  
      table = "taxiScoreOutput"  )  
    ```  
    + 为了简化此示例，逻辑回归模型的输入与用于定型该模型的 `featureDataSource` 相同。  更通常的情况下，可能具有一些新数据要进行评分，或者可能已留出一些数据用于测试或训练。  
  
    + 预测结果保存在表 _taxiscoreOutput_中。 请注意，当使用 `rxSqlServerData`创建此表时，未定义其架构，但可以从 *的* scoredOutput `rxPredict`对象输出获取。  
  
    + 若要创建存储预测值的表，运行 `rxSqlServer` 数据函数的 SQL 登录名必须在数据库中具有 DDL 特权。 如果登录名不能创建表，该语句则将失败。  
  
2.  调用 *rxPredict* 函数以生成结果。  
  
    ```R  
    rxPredict(modelObject = logitObj, 
        data = featureDataSource, 
        outData = scoredOutput,   
        predVarNames = "Score", 
        type = "response",   
        writeModelVars = TRUE, overwrite = TRUE)  
    ```  

  
## <a name="plotting-model-accuracy"></a>绘制模型准确性图表  
若要了解模型的准确性，可使用 *rxRocCurve* 函数来绘制接收方操作曲线。 由于 *rxRocCurve* 是由支持远程计算上下文的 RevoScaleR 包提供的新函数之一，因此有两种选择：  
  
+ 你可以使用 `rxRocCurve` 函数在远程计算机上下文中执行该绘图，然后将绘图返回本地客户端。
+ 你还可以将数据导入 R 客户端计算机，并使用其他 R 绘图函数来创建性能图表。  
  
在本节内容中，你将使用这两种技术。  
  
### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>在远程 (SQL Server) 计算上下文中执行绘图  
  
1.  调用函数 *rxRocCurve* 并提供之前定义的数据作为输入。  
  
    ```R  
    rxRocCurve( "tipped", "Score", scoredOutput)  
    ```  
  
    请注意，你还必须指定小费（尝试预测的变量）标签列和存储该预测（_评分_）列的名称。  
  
2.  通过打开 R 图形设备，或在 RStudio 中单击“绘制”  窗口查看图形。  
  
    ![模型的 ROC 绘图](../../advanced-analytics/r-services/media/rsql-e2e-rocplot.png "模型的 ROC 绘图")  

    此图形在远程计算上下文中创建，然后返回到 R 环境。   
    
### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>使用 SQL Server 中的数据在本地计算上下文中创建绘图  
  
1.  使用 *rxImport* 函数，将指定数据引入本地 R 环境。  
  
    ```R  
    scoredOutput = rxImport(scoredOutput)  
    ```  
  
2.  将数据加载到本地内存后，可调用 **ROCR** 库来创建一些预测，并生成绘图。  
  
    ```R  
    library('ROCR')  
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped)  
  
    acc.perf = performance(pred, measure = 'acc')  
    plot(acc.perf)  
    ind = which.max( slot(acc.perf, 'y.values')[[1]] )  
    acc = slot(acc.perf, 'y.values')[[1]][ind]  
    cutoff = slot(acc.perf, 'x.values')[[1]][ind]  
    ```  
  
3.  这两种情况都将生成以下绘图。  
  
    ![使用 R 测绘模型性能](../../advanced-analytics/r-services/media/rsql-e2e-performanceplot.png "使用 R 测绘模型性能")  
  
## <a name="deploying-a-model"></a>部署模型  

构建模型并确定其运行良好之后，就可对该模型进行操作  。 因为 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 允许使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程调用 R 模型，在客户端应用程序中使用 R 非常容易。  
  
但是，从外部应用程序中调用模型之前，必须将模型保存到用于生产的数据库中。 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中，已定型的模型以二进制形式存储在 **varbinary(max)**类型的单个列中。

因此，将训练用模型从 R 移动到 SQL Server 的操作包括以下步骤：  
  
+ 将模型序列化为十六进制字符串
+ 将序列化的对象传输到数据库
+ 将模型保存在 varbinary(max) 列中  
  
在本部分中，你将学习如何保持该模型，以及如何调用它来进行预测。  
  
### <a name="serialize-the-model"></a>序列化模型  
  
+  在本地 R 环境中，序列化模型并将其保存在变量中。  
  
    ```R  
    modelbin <- serialize(logitObj, NULL)  
    modelbinstr=paste(modelbin, collapse="")  
    ```  
  
    *serialize* 函数已被纳入 R **基础** 包，并为序列化提供一个到连接的简单的低级别接口。 有关详细信息，请参阅 [http://www.inside-r.org/r-doc/base/serialize](http://www.inside-r.org/r-doc/base/serialize)。  
  
### <a name="move-the-model-to-sql-server"></a>将模型移动到 SQL Server

+ 打开一个 ODBC 连接，然后调用存储过程，将模型的二进制表现形式存储到数据库的列中。 
  
    ```R  
    library(RODBC)  
    conn <- odbcDriverConnect(connStr )  
  
    # persist model by calling a stored procedure from SQL  
    q\<-paste("EXEC PersistModel @m='", modelbinstr,"'", sep="")  
    sqlQuery (conn, q)    
    ```  

将模型保存到表仅需要 INSERT 语句。 但是，为了使其变得更简单，此处使用了 _PersistModel_ 存储过程。 
 
以下是供参考的存储过程完整代码：  
  
```tsql  
CREATE PROCEDURE [dbo].[PersistModel]  @m nvarchar(max)  
AS  
BEGIN  
        -- SET NOCOUNT ON added to prevent extra result sets from  
        -- interfering with SELECT statements.  
        SET NOCOUNT ON;  
        insert into nyc_taxi_models (model) values (convert(varbinary(max),@m,2))  
END   
```  
> [!TIP]
> 建议创建 helper 函数（例如此存储过程），以便更轻松地在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中管理和更新 R 模型。  
  
  
### <a name="invoke-the-saved-model"></a>调用已保存的模型  
将模型保存到数据库后，你可以使用系统存储过程 [sp_execute_external_script (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 从 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码中对其进行直接调用。  
  
例如，若要生成预测，你只需连接到数据库并运行使用已保存的模型作为输入的存储过程，以及一些输入的数据。  
  
但是，如果你有经常使用的模型，在自定义存储过程中，将输入查询和对该模型以及任何其他参数的调用包装起来则会更加容易。  
  
在下一课中，你将学习如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]针对已保存的模型进行评分。  
  
## <a name="next-lesson"></a>下一课  
[第 5 课：部署和使用模型（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-5-deploy-and-use-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>前一课  
[第 3 课：创建数据功能（数据科学端到端演练）](../../advanced-analytics/r-services/lesson-3-create-data-features-data-science-end-to-end-walkthrough.md)  
  
  
  


