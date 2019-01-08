---
title: 生成 R 模型并保存到 SQL Server （演练）-SQL Server 机器学习
description: 本教程介绍如何构建用于 SQL Server 数据库内分析 R 语言模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b02b1e0298af6fbb96ba5ddd8d5a18dc8e154598
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645476"
---
# <a name="build-an-r-model-and-save-to-sql-server-walkthrough"></a>生成 R 模型并保存到 SQL Server （演练）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在此步骤中，了解如何生成机器学习模型并将模型保存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 通过保存模型时，你可以调用它直接从[!INCLUDE[tsql](../../includes/tsql-md.md)]使用系统存储过程的代码[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)或[PREDICT (T-SQL) 函数](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)。

## <a name="prerequisites"></a>先决条件

此步骤假定正在进行 R 会话基于本演练中之前的步骤。 它使用这些步骤中创建的连接字符串和数据源对象。 使用以下工具和包来运行脚本。

+ 若要运行 R 命令的 Rgui.exe
+ Management Studio 来运行 T-SQL
+ ROCR 包
+ RODBC 包

### <a name="create-a-stored-procedure-to-save-models"></a>创建用于保存模型的存储的过程

此步骤中使用存储的过程以将已训练的模型保存到 SQL Server。 创建存储的过程来执行此操作使任务更容易。

在查询窗口中查看 Management Studio 来创建存储的过程中运行以下 T-SQL 代码。

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
> 如果遇到错误，请确保您的登录名有权创建对象。 您可以授予显式权限，通过运行类似如下的 T-SQL 语句创建对象： `exec sp_addrolemember 'db_owner', '<user_name>'`。

## <a name="create-a-classification-model-using-rxlogit"></a>创建分类模型使用 rxLogit

该模型是二元分类器预测出租车司机是否有可能要或不获取某次搭乘的提示。 将使用你在上一课中来定型小费分类器，创建使用逻辑回归的数据源。

1. 调用包括在 [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit) 包中的 **rxLogit** 函数，创建逻辑回归模型。 

    ```R
    system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource));
    ```

    生成模型的调用封装在 system.time 函数中。 这样，你便可获得生成模型所需的时间。

2. 生成模型后，你可以进行检查，使用`summary`函数，并查看系数。

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

1. 首先，使用[RxSqlServerData](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqlserverdata)函数，以定义一个用于存储评分结果的数据源对象。

    ```R
    scoredOutput <- RxSqlServerData(
      connectionString = connStr,
      table = "taxiScoreOutput"  )
    ```

    + 若要简化此示例中，逻辑回归模型的输入是相同的功能的数据源 (`sql_feature_ds`) 用于为模型定型。  更通常的情况下，可能具有一些新数据要进行评分，或者可能已留出一些数据用于测试或训练。
  
    + 预测结果将保存在表中， _taxiscoreOutput_。 请注意，它使用 rxSqlServerData 创建时未定义此表的架构。 RxPredict 输出中获取该架构。
  
    + 若要创建存储预测的值的表，运行 rxSqlServer 数据函数的 SQL 登录名必须在数据库中具有 DDL 特权。 如果该登录名不能创建表，该语句将失败。

2. 调用 [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict) 函数以生成结果。

    ```R
    rxPredict(modelObject = logitObj,
        data = featureDataSource,
        outData = scoredOutput,
        predVarNames = "Score",
        type = "response",
        writeModelVars = TRUE, overwrite = TRUE)
    ```
    
    如果该语句成功，需要一些时间才能运行。 完成后，可以打开 SQL Server Management Studio，并验证该表的创建，并且它包含评分列和其他所需的输出。

## <a name="plot-model-accuracy"></a>绘制模型准确性。

若要了解模型的准确性，可以使用[rxRoc](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxroc)函数来绘制接受者操作曲线。 由于 rxRoc 是由 RevoScaleR 包提供的新函数之一支持远程计算上下文，有两个选项：

+ RxRoc 函数可用于在远程计算上下文中执行该绘图，然后将绘图返回本地客户端。

+ 你还可以将数据导入 R 客户端计算机，并使用其他 R 绘图函数来创建性能图表。

在本部分中，您将体验这两种技术。

### <a name="execute-a-plot-in-the-remote-sql-server-compute-context"></a>在远程 (SQL Server) 计算上下文中执行绘图

1. 调用函数 rxRoc 并提供作为输入前面定义的数据。

    ```R
    scoredOutput = rxImport(scoredOutput);
    rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    ```

    此调用将返回计算 ROC 图表中使用的值。 标签列_tipped_，其中包含要预测，实际结果时_分数_列的预测。

2. 若要实际绘制图表，可以保存 ROC 对象并与绘图函数然后绘制它。 在关系图创建远程计算上下文，并返回到你的 R 环境。

    ```R
    scoredOutput = rxImport(scoredOutput);
    rocObjectOut <- rxRoc(actualVarName= "tipped", predVarNames = "Score", scoredOutput);
    plot(rocObjectOut);
    ```

    通过打开 R 图形设备，或通过单击查看关系图**绘制**在 RStudio 中的窗口。

    ![模型的 ROC 绘图](media/rsql-e2e-rocplot.png "模型的 ROC 绘图")

### <a name="create-the-plots-in-the-local-compute-context-using-data-from-sql-server"></a>使用 SQL Server 中的数据在本地计算上下文中创建绘图

你可以验证计算上下文位于本地的通过运行`rxGetComputeContext()`在命令提示符处。 返回值应为"RxLocalSeq 计算上下文"。

1. 对于本地计算上下文，该过程是大致相同。 您使用[rxImport](https://docs.microsoft.com/r-server/r-reference/revoscaler/rximport)函数将指定的数据引入本地 R 环境。

    ```R
    scoredOutput = rxImport(scoredOutput)
    ```

2. 在本地内存中使用的数据，加载**ROCR**包，并使用来自该包的预测函数来创建一些新的预测。

    ```R
    library('ROCR');
    pred <- prediction(scoredOutput$Score, scoredOutput$tipped);
    ```

3. 生成本地绘图，基于输出变量中存储的值`pred`。

    ```R
    acc.perf = performance(pred, measure = 'acc');
    plot(acc.perf);
    ind = which.max( slot(acc.perf, 'y.values')[[1]] );
    acc = slot(acc.perf, 'y.values')[[1]][ind];
    cutoff = slot(acc.perf, 'x.values')[[1]][ind];
    ```

    ![使用 R 测绘模型性能](media/rsql-e2e-performanceplot.png "使用 R 测绘模型性能")

> [!NOTE]
> 图表的外观可能有所不同，这取决于您使用多少数据点。

## <a name="deploy-the-model"></a>部署模型

生成一个模型并已确定其运行良好之后，你可能想要将其部署到使用该模型，或可能是重新训练和重新校准定期模型用户或组织中的人员可以在此处进行的站点。 此过程有时称为*实施*模型。 在 SQL Server 中，操作化是通过将 R 代码嵌入在存储过程中实现的。 代码驻留在该过程，因为它可以从任何应用程序可以连接到 SQL Server 调用。

从外部应用程序中调用模型之前，你必须将模型保存到用于生产的数据库。 训练的模型存储在类型的单个列中的二进制格式**varbinary （max)**。

典型的部署工作流包括以下步骤：

1. 将模型序列化到十六进制字符串
2. 传输到数据库的序列化的对象
3. 将模型保存在 varbinary （max） 列

在本部分中，了解如何使用存储的过程来保持该模型并使其可用于预测。 在本部分中使用的存储的过程是 PersistModel。 PersistModel 的定义位于[先决条件](#prerequisites)。

1. 切换回在本地 R 环境中，如果你尚未使用它，序列化模型，并将其保存在变量中。

    ```R
    rxSetComputeContext("local");
    modelbin <- serialize(logitObj, NULL);
    modelbinstr=paste(modelbin, collapse="");
    ```

2. 打开 ODBC 连接使用**RODBC**。 如果已加载的包，则可以省略 rodbc 调用。

    ```R
    library(RODBC);
    conn <- odbcDriverConnect(connStr);
    ```

3. 调用 PersistModel 存储过程在 SQL Server 上 transmite 到数据库的序列化的对象并将该模型的二进制表示形式存储在列中。 

    ```R
    q <- paste("EXEC PersistModel @m='", modelbinstr,"'", sep="");
    sqlQuery (conn, q);
    ```

4. 使用 Management Studio 验证模型存在。 在对象资源管理器，右键单击**nyc_taxi_models**表，然后单击**选择前 1000年行**。 应在结果中，请参阅中的二进制表示形式**模型**列。

将模型保存到表仅需要 INSERT 语句。 但是，通常很容易时包装在存储过程，如*PersistModel*。

## <a name="next-steps"></a>后续步骤

在下一步也是最后一课中，了解如何执行针对已保存的模型使用评分[!INCLUDE[tsql](../../includes/tsql-md.md)]。

> [!div class="nextstepaction"]
> [部署 R 模型，在 SQL 中使用](walkthrough-deploy-and-use-the-model.md)
