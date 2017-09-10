---
title: "更新-为 SQL Server 文档高级分析 |Microsoft 文档"
description: "显示更新内容的最近更改中的文档，为 Microsoft SQL server 的高级分析的代码的段。"
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/17/2017
ms.author: genemi
ms.workload: advanced-analytics
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 79f979ecda1ff0851978d19ef28fa3cf909f9a43
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>新的和最近的更新： SQL Server 的高级分析



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- *更新日期范围：*&nbsp;从 2017-05-23&nbsp; 到 2017-07-17&nbsp;
- *主题区域：* &nbsp; **for SQL Server 的高级分析**。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [外部脚本执行的常见问题](common-issues-external-script-execution.md)
2. [用于机器学习故障排除数据收集](data-collection-ml-troubleshooting-process.md)
3. [SQL Server Python 教程](tutorials/sql-server-python-tutorials.md)
4. [SQL Server R 教程](tutorials/sql-server-r-tutorials.md)




&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表提供了在摘要部分列出的所有更新文章的链接。



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分显示从最近大幅更新的文章中收集到的更新的摘录内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-introducing-revoscalepypythonwhat-is-revoscalepymd"></a>1.&nbsp;[简介 revoscalepy](python/what-is-revoscalepy.md)

更新日期：2017-06-23 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;（[下一篇](#TitleNum_2)）

<!-- Source markdown line 112.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 cab7330ac9944508aaa360e00cbc2e866455776d 33f4e0e2421fa79fc11931dc7f29bff4432c6f5a  (PR=2171  ,  Filename=what-is-revoscalepy.md  ,  Dirpath=docs\advanced-analytics\python\  ,  MergeCommitSha40=7d2dbe0bdc4cbd05f11eacf938b35a9c35ace2e7) -->



**使用 MicrosoftML revoscalepy**


MicrosoftML Python 函数与计算上下文和 revoscalepy 中提供的数据源集成。 因此，您无法使用 MicrosoftML 算法来定义并定型模型以 Python，并使用 revoscalepy 函数来执行 Python 代码，本地或在 SQl Server 计算上下文中。

仅导入你的 Python 代码中的模块，然后引用所需的各个功能。

```
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

**要求**


若要在 SQL Server 中运行 Python 代码，你必须已安装 SQL Server 2017 与功能结合**机器学习服务**，并启用 Python 的语言。 早期版本的 SQL Server 不支持 Python 集成。

> [!NOTE]
> Python 的开源分发不支持 SQL Server 计算上下文。 但是，如果你需要发布和使用在 Windows 中的 Python 应用程序，你可以安装 Microsoft 机器学习服务器而无需安装 SQL Server。 有关详细信息，请参阅 [创建独立 R Server.../r/create-a-standalone-r-server.md)

**获取更多帮助**





&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-step-5-train-and-save-a-model-using-t-sqltutorialssqldev-py5-train-and-save-a-model-using-t-sqlmd"></a>2.&nbsp;[步骤 5： 训练和使用 T-SQL 的保存的模型](tutorials/sqldev-py5-train-and-save-a-model-using-t-sql.md)

*更新时间： 2017年-06-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 121.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5c1cbe92282b96105ffdb69efa803f58dc0ac7e2 e4077a2154a90de468c435efa5b2225125d5b0e7  (PR=1904  ,  Filename=sqldev-py5-train-and-save-a-model-using-t-sql.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=dbf91e0d6f8257227cfe8ac6d13c484d0a566f57) -->



1. 在 [！包括 [ssManStudio.../../includes/ssmanstudio-md.md)]，打开一个新查询窗口并运行以下语句以创建存储的过程_TrainTipPredictionModelRxPy_。  此模型将基于定型数据只是准备。 由于存储的过程已包含的输入数据的定义，不需要提供的输入的查询。

    ```SQL
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelRxPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelRxPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script 
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    import pandas
    from revoscalepy.functions.RxLogit import rx_logit_ex
    
    ## Create a logistic regression model using rx_logit_ex function from revoscalepy package
    logitObj = rx_logit_ex("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
    ## Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    ```



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-step-6-operationalize-the-modeltutorialssqldev-py6-operationalize-the-modelmd"></a>3.&nbsp;[步骤 6： 实施该模型](tutorials/sqldev-py6-operationalize-the-model.md)

*更新时间： 2017年-06-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_2) | [下一步](#TitleNum_4))

<!-- Source markdown line 236.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1eb50ac902d4e80bafb1dd7fdf8f607dcdf0d33f 57d5abdc6119db1ecd81587d625054a5bbfb5fc8  (PR=1904  ,  Filename=sqldev-py6-operationalize-the-model.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=dbf91e0d6f8257227cfe8ac6d13c484d0a566f57) -->



下面是执行评分使用存储过程的定义**revoscalepy**模型。

```
CREATE PROCEDURE [dbo].[PredictTipSingleModeRxPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
    SELECT * FROM [dbo].[fnEngineerFeatures-- 
      @passenger_count,
      @trip_distance,
      @trip_time_in_secs,
      @pickup_latitude,
      @pickup_longitude,
      @dropoff_latitude,
      @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      from revoscalepy.functions.RxPredict import rx_predict_ex;
```




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-use-python-with-revoscalepy-to-create-a-modeltutorialsuse-python-revoscalepy-to-create-modelmd"></a>4.&nbsp;[使用 Python 与 revoscalepy 来创建模型](tutorials/use-python-revoscalepy-to-create-model.md)

*更新时间： 2017年-06-21* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_3))

<!-- Source markdown line 119.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0886939f86fe12d7ff7b339689a02c7fc75e0786 23dd469349a05d535063aab3c14aec152ed2cd7b  (PR=2141  ,  Filename=use-python-revoscalepy-to-create-model.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=76839e39427e24688609353b8708d59fee772d28) -->



**查看代码**


让我们查看代码并突出显示一些关键步骤。

**定义数据源，并计算上下文**


这是使用的重要组成部分**revoscalepy**和其相关的 R 包**RevoScaleR**。 数据源是不同的计算上下文。 _数据源_定义在代码中使用的数据。 _计算上下文_定义才能执行的代码。

> [!NOTE]
> 对于在 RevoScaleR 中受支持的某些数据源类型的支持可能受限的预发行版本。 有关最新版本中包括的函数的详细信息，请参阅 [什么是...revoscalepy-/python/what-is-revoscalepy.md)。

整体进程进行创建和使用数据源，并计算上下文的是，如下所示：

1. 创建 Python 变量，如_sqlQuery_和_connectionString_，定义在源和你想要使用的数据。 将对这些变量传递**RxSqlServerData**构造函数来实现**数据源对象**名为_数据源_。
2. 通过创建计算上下文对象**RxInSqlServer**构造函数。 在此示例中，你将传递定义你将使用作为计算上下文的相同 SQL Server 实例上的数据是假定的更早版本，相同的连接字符串。 但是，数据源和计算上下文可能在不同服务器上。 生成**计算上下文对象**名为_computeContext_。
3. 选择的主动计算上下文。 默认情况下，操作在本地运行，这意味着，如果没有指定不同的计算上下文、 将从数据源提取数据和模型调整将在你当前的 Python 环境中运行。

    在 RevoScaleR，你还可以使用该函数`rxSetComputeContext`计算上下文之间进行切换。 函数中的预览版本未尚未实现**revoscalepy**，但你可以指定用作的自变量的计算上下文**rx_lin_mod_ex**。





<a name="similars2"/>

&nbsp;

## <a name="similar-articles"></a>类似文章

本节针对同一 GitHub.com 存储库 ([MicrosoftDocs/**sql-docs-pr**](https://github.com/microsoftdocs/sql-docs-pr/)) 中其他主题区域的最近更新的文章列出了非常相似的文章。

<!--  20170717-1101  -->

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新的和更新的文章 (4+4)：Advanced Analystics for SQL 文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新的和更新的文章 (2+0)：Analysis Services for SQL 文档](../analysis-services/new-updated-analysis-services.md)
- [新的和更新的文章 (1+2)：连接到 SQL 文档](../connect/new-updated-connect.md)
- [新的和更新的文章 (6+0)：SQL 数据库引擎文档](../database-engine/new-updated-database-engine.md)
- [新的和更新的文章 (13+2)：Linux for SQL 文档](../linux/new-updated-linux.md)
- [新的和更新的文章 (1+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (1+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (8+4)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)
- [新的和更新的文章 (2+2)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)
- [新的和更新的文章 (0+1)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)
- [新的和更新的文章 (1+0)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)
- [新的和更新的文章 (1+0)：Tools for SQL 文档](../tools/new-updated-tools.md)


#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>没有新的或最近更新文章的主题区域

- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新的和更新的文章 (0+0)：Integration Services for SQL 文档](../integration-services/new-updated-integration-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新的和更新的文章 (0+0)：Reporting Services for SQL 文档](../reporting-services/new-updated-reporting-services.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../sample/new-updated-sample.md)
- [新的和更新的文章 (0+0)：SQL Server Data Tools (SSDT) 文档](../ssdt/new-updated-ssdt.md)
- [新的和更新的文章 (0+0)：SQL Server Migration Assistant (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)


&nbsp;


