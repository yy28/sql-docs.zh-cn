---
title: "生成 R 模型并将保存到 SQL Server |Microsoft 文档"
ms.custom: 
ms.date: 07/14/2017
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
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 437ec62abb0107e8a70926fd60d0c54cc6064122
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="build-an-r-model-and-save-to-sql-server"></a>生成 R 模型并将保存到 SQL Server

在此步骤中，您将学习如何生成机器学习模型，并将保存在模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

## <a name="create-a-classification-model-using-rxlogit"></a>创建使用 rxLogit 的分类模型

生成该模型是预测 taxi 驱动程序是否有可能，若要获取特定的持续一段时间的提示，或不二元分类器。 你将使用你在上一课中训练提示分类器，创建使用逻辑回归的数据源。

1. 调用包括在 [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) 包中的 **rxLogit** 函数，创建逻辑回归模型。 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = sql_feature_ds));
    ```

    生成模型的调用封装在 system.time 函数中。 这样，你便可获得生成模型所需的时间。

2. 生成模型后，你可以检查它使用`summary`函数，并查看系数。

    ```R
    summary(logitObj);
    ```

     *结果*

     *逻辑回归结果： 附属式 ~ passenger_count + trip_distance + trip_time_in_secs +*
     <br/>*direct_distance*
     <br/>*数据： featureDataSource （RxSqlServerData 数据源）*
     <br/>*Dependent variable(s)： 附属式*
     <br/>*自变量的总： 5*
     <br/>*有效的观测值的数目： 17068*
     <br/>*缺少观察值： 0*
     <br/>*-2\*LogLikelihood: 23540.0602 （残留偏差 17063 自由度上）*
     <br/>*系数：*
     <br/>*Estimate Std.错误 z 值 Pr (> | z |)*
     <br/>*（截获）-2.509e-03 3.223e-02-0.078 0.93793*
     <br/>*passenger_count-5.753e-02 1.088e-02-5.289 1.23 e-07\*\*\**
     <br/>*trip_distance-3.896e-02 1.466e-02-2.658 0.00786\*\**
     <br/>*trip_time_in_secs 2.115e-04 4.336e-05 4.878 1.07e-06\*\*\**
     <br/>*direct_distance 6.156e-02 2.076e-02 2.966 0.00302\*\**
     <br/>*---*
     <br/>*Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’0.1 ‘ ’ 1*
     <br/>*条件的最终的方差协方差矩阵数： 48.3933*
     <br/>*Number of iterations: 4*

## <a name="use-the-logistic-regression-model-for-scoring"></a>使用逻辑回归模型进行计分

既然已生成模型，可以用其来预测出租车司机是否有可能在某次搭乘中获得小费。

1. 首先，使用[RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata)函数定义一个用于存储评分 resul 的数据源对象

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + 若要使此示例更简单，逻辑回归模型的输入是相同的功能数据源 (`sql_feature_ds`) 你用来训练该模型。  更通常的情况下，可能具有一些新数据要进行评分，或者可能已留出一些数据用于测试或训练。
  
    + 预测结果将保存在表中， _taxiscoreOutput_。 请注意当你创建使用 rxSqlServerData 未定义此表的架构。 RxPredict 输出中获取的架构。
  
    + 要创建存储的预测的值的表，运行 rxSqlServer 数据函数的 SQL 登录名必须在数据库中拥有 DDL 权限。 如果登录名不能创建表，该语句将失败。

2. 调用 [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) 函数以生成结果。

    ```R
    rxPredict(modelObject = logitObj,
        data = sql_feature_ds,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    如果该语句会成功，则应需要一些时间才能运行。 完成后，你可以打开 SQL Server Management Studio，并验证表创建，并且它包含评分列和其他所需的输出。

## <a name="plot-model-accuracy"></a>绘制模型准确性

若要了解模型的准确性，可以使用[rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc)函数进行绘图时接收方运行曲线。 因为 rxRoc 是由 RevoScaleR 包提供的新函数之一并支持远程计算上下文，有两个选项：

+ RxRoc 函数可用于远程计算上下文中执行该绘图，然后返回到本地客户端的该绘图。

+ 你还可以将数据导入 R 客户端计算机，并使用其他 R 绘图函数来创建性能图表。

在此部分中，将使用这两种方法中进行试验。

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>在远程 (SQL Server) 计算上下文中执行绘图

1. 调用函数 rxRoc 并提供作为输入前面定义的数据。

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    此调用将返回计算 ROC 图表中使用的值。 标签列_附属式_，它具有你尝试预测的实际结果时_分数_列的预测。

2. 若要实际绘制图表，可以保存 ROC 对象，然后将其与拖`plot`函数。 关系图上远程计算上下文中，创建并返回到 R 环境。

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    通过打开 R 图形设备，或通过单击查看关系图**绘制**中 RStudio 窗口。

    ![模型的 ROC 绘图](media/rsql-e2e-rocplot.png "模型的 ROC 绘图")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>使用 SQL Server 中的数据在本地计算上下文中创建绘图

1. 对于本地计算上下文，该过程是大致相同。 你使用[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport)函数将指定的数据引入本地 R 环境。

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. 在本地内存中使用的数据，加载**ROCR**包，并从该程序包的预测函数用于创建一些新的预测。

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);

3. Generate a local plot, based on the values stored in the output variable `pred`.

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![使用 R 测绘模型性能](media/rsql-e2e-performanceplot.png "使用 R 测绘模型性能")

> [!NOTE]
> 你的图表外观可能有所不同，这取决于你使用的多少数据点。

## <a name="deploy-the-model"></a>部署模型

在生成模型并确定运行良好后，你可能想要将其部署到用户或组织中的人员可以在此处进行使用该模型，或可能重新训练，重新校准定期模型时的站点。 此过程有时称为*留给*模型。

因为[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]允许调用 R 模型使用[!INCLUDE[tsql](../../includes/tsql-md.md)]很容易在客户端应用程序中使用 R 的存储的过程。

但是，从外部应用程序中调用模型之前，必须将模型保存到用于生产的数据库中。 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]中，已定型的模型以二进制形式存储在 **varbinary(max)**类型的单个列中。

因此，将训练用模型从 R 移动到 SQL Server 的操作包括以下步骤：

+ 将模型序列化为十六进制字符串

+ 将序列化的对象传输到数据库

+ 将模型保存在 varbinary(max) 列中

在本部分中，你将了解如何保留模型，以及如何调用它来进行预测。

1. 切换回本地 R 环境中，如果你尚未使用它、 序列化模型，并将其保存在变量中。

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. 打开 ODBC 连接使用**RODBC**。

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

    如果你已加载的包，则可以省略到 RODBC 调用。

3. 调用 PowerShell 脚本，在数据库中的列中存储的二进制表示形式模型创建的存储的过程。

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

    将模型保存到表仅需要 INSERT 语句。 但是，很容易时包装在存储过程中，如_PersistModel_。

    > [!NOTE]
    > 如果你收到如下错误"的 EXECUTE 权限拒绝了对对象 PersistModel"，请确保你的登录名具有的权限。 可以通过运行类似的 T-SQL 语句授予显式权限，只需对存储过程：`GRANT EXECUTE ON [dbo].[PersistModel] TO <user_name>`

4. 创建模型并将其保存在数据库中，你可以调用它直接从后[!INCLUDE[tsql](../../includes/tsql-md.md)]代码，使用系统存储过程中， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

    但是，与你通常使用任何模型，是更轻松地将输入的查询和对模型，以及其他参数的调用包装在自定义的存储过程。

    下面是一个此类存储过程的完整代码。 我们建议创建诸如此类以使其更轻松地管理和更新 R 模型中的存储的过程[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

    ```tsql
    CREATE PROCEDURE [dbo].[PersistModel]  @m nvarchar(max)
    AS
    BEGIN
      SET NOCOUNT ON;
      INSERT INTO nyc_taxi_models (model) values (convert(varbinary(max),@m,2))
    END
    ```

  > [!NOTE]
  > 使用**SET NOCOUNT ON**子句以防止额外结果设置妨碍的 SELECT 语句。


在下一步，也是最后课中，了解如何执行针对已保存的模型使用评分[!INCLUDE[tsql](../../includes/tsql-md.md)]。

## <a name="next-lesson"></a>下一课

[在 SQL 部署 R 模型和使用](/walkthrough-deploy-and-use-the-model.md)

## <a name="previous-lesson"></a>上一课

[创建使用 R 和 SQL 数据功能](/walkthrough-create-data-features.md)


