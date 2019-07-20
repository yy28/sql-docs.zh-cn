---
title: 生成 R 模型并保存到 SQL Server (演练)
description: 介绍如何生成用于 SQL Server 数据库内分析的 R 语言模型的教程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: eec6d165b8e3aa4130246aae6d4aaf5b4102fc0f
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345823"
---
# <a name="build-an-r-model-and-save-to-sql-server-walkthrough"></a>生成 R 模型并保存到 SQL Server (演练)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在此步骤中, 将了解如何生成机器学习模型并将模型保存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中。 通过保存模型, 可以使用系统存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)或[!INCLUDE[tsql](../../includes/tsql-md.md)] [PREDICT (t-sql) 函数](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)直接从代码调用它。

## <a name="prerequisites"></a>先决条件

此步骤假设正在进行的 R 会话基于本演练中前面的步骤。 它使用在这些步骤中创建的连接字符串和数据源对象。 以下工具和包用于运行脚本。

+ Rgui.exe 运行 R 命令
+ Management Studio 运行 T-sql
+ ROCR 包
+ RODBC 包

### <a name="create-a-stored-procedure-to-save-models"></a>创建存储过程以保存模型

此步骤使用存储过程将定型模型保存到 SQL Server。 创建存储过程来执行此操作可使任务更容易。

在 Management Studio 中的查询窗口中运行以下 T-sql 代码, 以创建存储过程。

```sql
USE [NYCTaxi_Sample]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO

IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PersistModel')
  DROP PROCEDURE PersistModel
GO

CREATE PROCEDURE [dbo].[PersistModel] @m nvarchar(max)
AS
BEGIN
    -- SET NOCOUNT ON added to prevent extra result sets from
    -- interfering with SELECT statements.
    SET NOCOUNT ON;
    insert into nyc_taxi_models (model) values (convert(varbinary(max),@m,2))
END
GO
```

> [!NOTE]
> 如果遇到错误, 请确保您的登录名具有创建对象的权限。 通过运行 T-sql 语句 (如下所示`exec sp_addrolemember 'db_owner', '<user_name>'`), 可以授予显式权限来创建对象。

## <a name="create-a-classification-model-using-rxlogit"></a>使用 rxLogit 创建分类模型

该模型是一个二元分类器, 可预测出租车驱动程序是否可能在特定行程上获得提示。 您将使用在上一课中创建的数据源, 使用逻辑回归训练 tip 分类器。

1. 调用包括在 [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) 包中的 **rxLogit** 函数，创建逻辑回归模型。 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource));
    ```

    生成模型的调用封装在 system.time 函数中。 这样，你便可获得生成模型所需的时间。

2. 生成模型后, 可以使用函数对`summary`其进行检查, 并查看系数。

    ```R
    summary(logitObj);
    ```

    **结果**
    
    ```R
     *Logistic Regression Results for: tipped ~ passenger_count + trip_distance + trip_time_in_secs +*
     direct_distance* 
     *Data: featureDataSource (RxSqlServerData Data Source)*
     *Dependent variable(s): tipped*
     *Total independent variables: 5*
     *Number of valid observations: 17068*
     *Number of missing observations: 0*
     *-2\*LogLikelihood: 23540.0602 (Residual deviance on 17063 degrees of freedom)*
     *Coefficients:*
     *Estimate Std. Error z value Pr(>|z|)*
     *(Intercept)       -2.509e-03  3.223e-02  -0.078  0.93793*
     *passenger_count   -5.753e-02  1.088e-02  -5.289 1.23e-07 \*\*\**
     *trip_distance     -3.896e-02  1.466e-02  -2.658  0.00786 \*\**
     *trip_time_in_secs  2.115e-04  4.336e-05   4.878 1.07e-06 \*\*\**
     *direct_distance    6.156e-02  2.076e-02   2.966  0.00302 \*\**
     *---*
     *Signif. codes:  0 ‘\*\*\*’ 0.001 ‘\*\*’ 0.01 ‘\*’ 0.05 ‘.’ 0.1 ‘ ’ 1*
     *Condition number of final variance-covariance matrix: 48.3933*
     *Number of iterations: 4*
   ```

## <a name="use-the-logistic-regression-model-for-scoring"></a>使用逻辑回归模型进行计分

既然已生成模型，可以用其来预测出租车司机是否有可能在某次搭乘中获得小费。

1. 首先, 使用[RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata)函数定义用于存储评分结果的数据源对象。

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + 为了使此示例更简单, 逻辑回归模型的输入与用于训练模型的功能数据源`sql_feature_ds`() 相同。  更通常的情况下，可能具有一些新数据要进行评分，或者可能已留出一些数据用于测试或训练。
  
    + 预测结果将保存在表_taxiscoreOutput_中。 请注意, 使用 rxSqlServerData 创建该表时, 未定义此表的架构。 该架构是从 rxPredict 输出获取的。
  
    + 若要创建存储预测值的表, 运行 rxSqlServer 数据函数的 SQL 登录名必须在数据库中具有 DDL 权限。 如果登录名不能创建表, 则语句将失败。

2. 调用 [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) 函数以生成结果。

    ```R
    rxPredict(modelObject = logitObj,
        data = featureDataSource,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    如果语句成功, 将需要一段时间才能运行。 完成后, 您可以打开 SQL Server Management Studio 并验证该表是否已创建, 并且它包含计分列和其他预期输出。

## <a name="plot-model-accuracy"></a>绘图模型准确性

若要了解模型的准确性, 可以使用[rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc)函数来绘制接收方操作曲线。 因为 rxRoc 是支持远程计算上下文的 RevoScaleR 包提供的新函数之一, 所以有两个选项:

+ 您可以使用 rxRoc 函数来执行远程计算上下文中的绘图, 然后将该绘图返回到本地客户端。

+ 你还可以将数据导入 R 客户端计算机，并使用其他 R 绘图函数来创建性能图表。

在本部分中, 你将尝试这两种方法。

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>在远程 (SQL Server) 计算上下文中执行绘图

1. 调用函数 rxRoc, 并提供之前定义为输入的数据。

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    此调用返回计算 ROC 图表时使用的值。 标签列是带标签的, 它具有您尝试预测的实际结果, 而_评分_列具有_预测值。_

2. 若要实际绘制图表, 可以保存该 ROC 对象, 然后用绘图函数进行绘制。 在远程计算上下文上创建图形, 并返回到 R 环境。

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    通过打开 R 图形设备, 或单击 RStudio 中的**绘图**窗口来查看图形。

    ![模型的 ROC 绘图](media/rsql-e2e-rocplot.png "模型的 ROC 绘图")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>使用 SQL Server 中的数据在本地计算上下文中创建绘图

可以通过在命令提示符下运行`rxGetComputeContext()`来验证计算上下文是否为本地计算上下文。 返回值应为 "RxLocalSeq 计算上下文"。

1. 对于本地计算上下文, 此过程几乎相同。 使用[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport)函数将指定的数据引入本地 R 环境。

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. 使用本地内存中的数据, 可以加载**ROCR**包, 并使用该包中的预测函数创建一些新的预测。

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. 基于输出变量`pred`中存储的值生成本地绘图。

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![使用 R 测绘模型性能](media/rsql-e2e-performanceplot.png "使用 R 测绘模型性能")

> [!NOTE]
> 图表可能与这些不同, 具体取决于使用的数据点数量。

## <a name="deploy-the-model"></a>部署模型

构建模型并已确定其执行良好后, 你可能想要将其部署到你的组织中的用户或人员可以使用该模型的站点, 或者可能会定期重新训练和重新校准模型。 此过程有时称为*实现*。 在 SQL Server 中, 操作化是通过在存储过程中嵌入 R 代码来实现的。 由于代码位于过程中, 因此可以从任何可以连接到 SQL Server 的应用程序调用它。

您必须将模型保存到用于生产的数据库中, 然后才能从外部应用程序调用该模型。 训练的模型以二进制形式存储在**varbinary (max)** 类型的单个列中。

典型的部署工作流包括以下步骤:

1. 将模型序列化为十六进制字符串
2. 将序列化的对象传输到数据库
3. 将模型保存在 varbinary (max) 列中

本部分介绍如何使用存储过程来持久保存模型并使其可用于预测。 本部分中使用的存储过程是 PersistModel。 PersistModel 的定义为[必备组件](#prerequisites)。

1. 如果尚未使用本地 R 环境, 请将其重新序列化, 并将其保存在变量中。

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. 使用**RODBC**打开 ODBC 连接。 如果已加载了包, 则可以省略对 RODBC 的调用。

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

3. 调用 SQL Server 上的 PersistModel 存储过程, 将序列化的对象 transmite 到数据库, 并将模型的二进制表示形式存储在列中。 

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

4. 使用 Management Studio 验证模型是否存在。 在对象资源管理器中, 右键单击**nyc_taxi_models**表, 然后单击 "**选择前1000行**"。 在结果中, 你应在 "**模型**" 列中看到二进制表示形式。

将模型保存到表仅需要 INSERT 语句。 但是, 在存储过程 (如*PersistModel*) 中包装时, 通常会更容易。

## <a name="next-steps"></a>后续步骤

在下一课和最后一课中, 了解如何使用[!INCLUDE[tsql](../../includes/tsql-md.md)]对保存的模型进行评分。

> [!div class="nextstepaction"]
> [在 SQL 中部署 R 模型并使用](walkthrough-deploy-and-use-the-model.md)
