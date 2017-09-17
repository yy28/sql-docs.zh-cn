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
ms.date: 09/11/2017
ms.author: genemi
ms.workload: advanced-analytics
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: fb6185aae04a1fb53a4db03cbab267e3f52dc779
ms.contentlocale: zh-cn
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>新的和最近的更新： SQL Server 的高级分析



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- *日期范围的更新：* &nbsp; **自 2017 年 1-07-18** &nbsp;到&nbsp;**自 2017 年 1-09-11**
- *主题区域：* &nbsp; **for SQL Server 的高级分析**。

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

以下链接跳转到最近已添加的新项目。


1. [如何执行实时评分或在 SQL Server 中的本机评分](r/how-to-do-realtime-scoring.md)
2. [安装预先训练的机器学习模型上 SQL Server](r/install-pretrained-models-sql-server.md)
3. [本机评分](sql-native-scoring.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分显示的摘自从最近出现了大规模更新的文章中收集的更新。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此 compact 列表提供了有关摘录部分中列出的所有更新的文章的链接。

1. [设置 Python 机器学习服务 （数据库）](#TitleNum_1)
2. [引入 revoscalepy](#TitleNum_2)
3. [不同 SQL Server 版本中机器学习功能的差异](#TitleNum_3)
4. [具有可操作性 R 代码 （机器学习服务）](#TitleNum_4)
5. [R 服务的性能： 结果和资源](#TitleNum_5)
6. [R Services-数据优化的性能](#TitleNum_6)
7. [SQL Server 的 R 包管理](#TitleNum_7)
8. [设置 SQL Server 机器学习服务（数据库内）](#TitleNum_8)
9. [与 R 一起使用的 SQL Server 配置](#TitleNum_9)
10. [SQL Server 中的 R 性能调整](#TitleNum_10)
11. [数据科学方案和解决方案模板](#TitleNum_11)
12. [什么是 SQL Server 中的机器学习服务中的新增功能](#TitleNum_12)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-set-up-python-machine-learning-services-in-databasepythonsetup-python-machine-learning-servicesmd"></a>1.&nbsp;[设置 Python 机器学习服务 （数据库）](python/setup-python-machine-learning-services.md)

*更新时间： 2017年-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([下一步](#TitleNum_2))

<!-- Source markdown line 263.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 fbe2ef55a5caecd64bb21ce854617a10b2d65567 8cd65baf77f27db00a0a4f07f3129a4231edb48b  (PR=3084  ,  Filename=setup-python-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\python\  ,  MergeCommitSha40=05976158e43d7dfafaf02289462d1537f5beeb36) -->



     [Modify the user account pool for SQL Server R Services--../r/modify-the-user-account-pool-for-sql-server-r-services.md)

如果你使用 SQL Server Standard Edition，并且没有资源调控器，可以使用动态管理视图和扩展的事件来帮助你管理服务器资源。 你还可以使用 Windows 事件监视为此目的。 有关详细信息，请参阅 [监视和管理 R 服务.../r/managing-and-monitoring-r-solutions.md)。

**升级机器学习组件**


通过使用 SQL Server 2017 安装机器学习服务时，你在已发布的发行版本时获得的组件的版本。 修补或升级的 SQL Server 实例，每次机器学习组件将同时升级。

你可以升级机器学习不支持的方式更快的定期的组件通过 SQL Server 版本中，通过安装 Microsoft 机器学习 Server。 执行此操作时，你还获得如在机器学习服务器的最新版本中受支持的任何新功能：

+ 更新的 Python 包[revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)和[for Python microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)。
+ [预先训练模型](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models)对图像分类和文本分析。

有关如何升级实例的信息，请参阅 [通过绑定-升级 R 组件...\r\use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)。

> [!NOTE]
>
> 当前的发行版本包含所有机学习组件的最新版本。 因此，尽管升级通过 Microsoft 机器学习服务器支持的 SQL Server 自 2017 年，当前可用升级仅适用于 SQL Server 2016 实例。



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-introducing-revoscalepypythonwhat-is-revoscalepymd"></a>2.&nbsp;[简介 revoscalepy](python/what-is-revoscalepy.md)

*更新时间： 自 2017 年-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_1) | [下一步](#TitleNum_3))

<!-- Source markdown line 79.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 33f4e0e2421fa79fc11931dc7f29bff4432c6f5a d2eac3313a74bc5d5afd754fc357b3693e6801e1  (PR=2939  ,  Filename=what-is-revoscalepy.md  ,  Dirpath=docs\advanced-analytics\python\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



| (第 1 列) | (column_2) | (column_3) |
| :-- | :-- | :-- |
|`rx_btrees` | 适合的随机渐变提升决策树|`rx_btrees_ex`在 CTP 2.0|
|`rx_dforest` | 适合分类和回归的决策林|`rx_dforest_ex`在 CTP 2.0|
|`rx_dtree` | 适合的分类和回归树 |`rx_dtree_ex`在 CTP 2.0|
|`rx_lin_mod` | 创建线性模型|`rx_lin_mod_ex`在 CTP 2.0|
|`rx_logit` | 创建逻辑回归模型|`rx_logit_ex`在 CTP 2.0|
|`rx_predict` | 从训练的模型生成预测|`rx_predict_ex`在 CTP 2.0|
|`rx_summary` | 生成模型的摘要||

新的机器学习算法还提供的 Python 版本[MicrosoftML](https://docs.microsoft.com/en-us/r-server/python-reference/microsoftml/microsoftml-package):

| 函数| Description|
| ------ | ------ |
|`rx_fast_forest` |创建决策林模型|
|`rx_fast_linear` | 使用随机双重坐标上升的线性回归|
|`rx_fast_trees` | 创建提升的树模型 |
|`rx_logistic_regression` | 创建逻辑回归模型|
|`rx_neural_network` | 创建一个可自定义神经网络模型 |
|`rx_oneclass_svm` | 在非平衡数据集，用于异常检测创建 SVM 模型|

> [!TIP]
> 许多这些算法已提供作为 Azure 机器学习中的模块。

For Python MicrosoftML 还包括各种转换和帮助器函数，如：

+ `rx_predict`从训练的模型生成预测，并可用于实时评分
+ 图像特征化函数
+ 文本处理和观点提取函数

有关详细信息，请参阅[MicrosoftML 简介](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)


> [!NOTE]
> Python 社区使用可能不同于你使用，包括所有小写字母和下划线，而对于参数名 camel 大小写的编码约定。 此外，可能是你已注意到， **revoscalepy**库始终采用小写形式。 没错！ 另一个 Python 约定。



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-differences-in-machine-learning-features-between-editions-of-sql-serverrdifferences-in-r-features-between-editions-of-sql-servermd"></a>3.&nbsp;[在机学习功能的 SQL Server 的版本之间的差异](r/differences-in-r-features-between-editions-of-sql-server.md)

*更新时间： 自 2017 年-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_2) | [下一步](#TitleNum_4))

<!-- Source markdown line 47.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b5890e212063f3ef228e69afe54e226320d2467f 4e0357701d960c0b8dbda1ac8d56a82f3335c77f  (PR=2964  ,  Filename=differences-in-r-features-between-editions-of-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=7b4f037616e0559ac62bbae5dbe04aeffe529b06) -->



     Only Express Edition with Advanced Services includes the machine learning features. The performance limitations are similar to Standard Edition. Web edition is not intended for tasks such as creating machine learning models; however, you can use the PREDICT function to perform scoring using models trained elsewhere.

-   **Azure SQL 数据库**

     Azure SQL 数据库中当前不支持机器学习功能，如 R 和 Python 脚本。

     有关详细信息，以及有关此功能何时可用，公告，请参阅 SQL Server 博客： [Python 中 SQL Server 2017： 增强数据库中机器学习](https://blogs.technet.microsoft.com/dataplatforminsider/2017/04/19/python-in-sql-server-2017-enhanced-in-database-machine-learning/)


**在所有版本中受支持的语言**


对于所有版本支持以下机器学习语言：

+ SQL Server 2017: R 和 Python
+ 仅 SQL Server 2016: R

所有版本都随附 Microsoft R Open。



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-operationalize-r-code-machine-learning-servicesroperationalizing-your-r-codemd"></a>4.&nbsp;[实施 R 代码 （机器学习服务）](r/operationalizing-your-r-code.md)

*更新时间： 2017年-07-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_3) | [下一步](#TitleNum_5))

<!-- Source markdown line 56.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7e11d9a5db93932ec89ca96b5337aa4ea03c1d13 0779f06444b5b73ae2dff8bc190d0e388b4ae8e7  (PR=2660  ,  Filename=operationalizing-your-r-code.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=70a1fd4dbec68d22187585de69a1d603c39e259e) -->



+ [实时.../ 实时一次性 scoring.md） 对于小的批处理评分，优化
+ 单行评分，用于从应用程序的调用
+ [本机评分.../ sql 本机 scoring.md），而不会调用 R 从 SQL Server 的快速的批处理预测

本演练提供了评分使用批处理和单行模式中的存储的过程的示例：

+ [端到端数据科学演练的中 SQL Server.../ tutorials/walkthrough-data-science-end-to-end-walkthrough.md）

请参阅如何集成应用程序中评分的示例这些解决方案模板：

+ [零售预测](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/RetailForecasting/Introduction.md)
+ [欺诈行为检测](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)
+ [群集的客户](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/getting-started/customer-clustering)

**提升性能和可扩展性**


尽管已知的开放源代码 R 语言有限制，RevoScaleR 包 Api 可以在大型数据集上运行并从中获益多线程、 多核、 多进程在数据库中计算。

如果 R 解决方案使用复杂的聚合或涉及到大型数据集，你可以利用 SQL Server 的高效率的内存中聚合和列存储索引，并让的 R 代码处理统计计算和评分。

有关如何改进 SQL Server 机器学习中的性能的详细信息，请参阅：

+ [性能优化的 SQL Server R 服务.../../ advanced-analytics/r/sql-server-r-services-performance-tuning.md）
+ [性能优化提示和技巧](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**调整为其他平台的 R 代码或计算上下文**




&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-performance-for-r-services-results-and-resourcesrperformance-case-study-r-servicesmd"></a>5.&nbsp;[R 服务的性能： 结果和资源](r/performance-case-study-r-services.md)

*更新时间： 2017年-07-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_4) | [下一步](#TitleNum_6))

<!-- Source markdown line 282.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 40c8cd255ead88edc60531d45dd0377ecbaf7c9b eeca5eed96e2223508910b246dbff18173eecea3  (PR=2565  ,  Filename=performance-case-study-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=cf8509cab2424529ca0ed16c936fa63a139dfca4) -->



对 RevoScaleR 和 MicrosoftML 封装了用于定型涉及大型数据集的复杂 R 解决方案中的预测模型。 SQL 查询和 R 代码都是相同。 已安装的 SQL server 的单个 Azure VM 上执行了所有测试。 作者然后进行比较，使用和不使用 SQL Server 提供的这些优化评分时间：

- 内存中表
- ssNoVersion
- 资源调控器

若要评估的软件 NUMA 对 R 脚本执行的影响，数据科学团队，请测试 20 的物理内核数与 Azure 虚拟机上安装解决方案。 在这些物理核心、 四个软件 NUMA 节点中，自动创建： 每个节点包含五个内核。

在恢复匹配方案中，以评估对 R 作业的影响强制实施 CPU 关联。 四个**SQL 资源池**和第四个**外部资源池**而创建，但未指定 CPU 关联，以确保将每个节点中使用一组相同的 Cpu。

每个资源池已分配给不同的工作负荷组中，以优化硬件利用率。 原因是该软件 NUMA 和 CPU 关联无法划分的物理 NUMA 节点; 中的物理内存因此，通过定义所有软 NUMA 节点基于同一个物理 NUMA 节点都必须使用内存在同一个操作系统内存块。 换而言之，没有任何内存到处理器的关联。

以下过程用于创建此配置：

1. 减少默认情况下分配给 SQL Server 的内存量。

2. 创建用于并行运行 R 作业的四个新池。

3. 创建四个工作负荷组，以便每个工作负荷组都与资源池相关联。

4. 使用新的工作负荷组和分配，重新启动资源调控器。

5. 创建用户定义的分类器函数 (UDF) 可分配给不同的工作负荷组上的不同任务。

6. 更新资源调控器配置，以对相应的工作负荷组使用的函数。



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-performance-for-r-services---data-optimizationrr-and-data-optimization-r-servicesmd"></a>6.&nbsp;[R Services-数据优化的性能](r/r-and-data-optimization-r-services.md)

*更新时间： 2017年-07-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_5) | [下一步](#TitleNum_7))

<!-- Source markdown line 107.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2ae2e54e8c5c8a3ec92fd2017088dd6ee879a9a1 9cb06bdce4ad6dfa2e9dc19da49103a6cd9817b3  (PR=2565  ,  Filename=r-and-data-optimization-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=cf8509cab2424529ca0ed16c936fa63a139dfca4) -->



> 如果在数据源而不是查询中指定了表，R Services 将使用内部试探法来确定要从表; 获取的必需列但是，这种方法是不太可能导致并行执行。

若要确保可以并行分析数据，用于检索数据的查询应分帧数据库引擎可以创建并行查询计划的方式。 如果代码或算法使用的大量数据，请确保提供给查询`RxSqlServerData`非常适合并行执行。 无法生成并行执行计划的查询可能会导致计算单个进程。

如果你需要处理大型数据集，使用 Management Studio 或另一个 SQL 查询分析器中的运行 R 代码，请先分析的执行计划。 然后，执行任何建议的步骤来提高查询性能。 例如，表中的缺失某个索引可能会影响执行查询所要花费的时间。 有关详细信息，请参阅 [监视器，并进行调整以获得性能.../../ relational-databases/performance/monitor-and-tune-for-performance.md）。

可能会影响性能的另一个常见错误是查询检索多于所需的列数。 例如，如果公式基于只有三个列，但你源表具有 30 列，您正在不必要地移动数据。

 + 避免使用`SELECT *`！
 + 需要一些时间来查看数据集中的列并确定只有所需的分析
 + 从你的查询中删除任何包含与 R 代码，例如 GUID 和 rowguid 不兼容的数据类型的列
 + 检查不受支持的日期和时间格式
 + 而不是加载表，创建一个视图，选择特定值或强制转换列，以免转换错误

**优化机器学习算法**


本部分提供的其他提示和特定于 RevoScaleR 和 Microsoft。 中的其他选项的资源



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-r-package-management-for-sql-serverrr-package-management-for-sql-server-r-servicesmd"></a>7.&nbsp;[For SQL Server 的 R 包管理](r/r-package-management-for-sql-server-r-services.md)

*更新时间： 自 2017 年-08-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_6) | [下一步](#TitleNum_8))

<!-- Source markdown line 22.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2add5a7e1aef02487ac875e353c51161658050a4 5da92dd8b5402266a837172bda9aaabed3162ce8  (PR=2939  ,  Filename=r-package-management-for-sql-server-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=91098c850b0f6affb8e4831325d0f18fd163d71a) -->



本主题介绍可用于管理 SQL server 的实例运行的 R 包的包管理功能。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务

**使用 T-SQL 的管理包**


你可以继续以管理员身份的计算机上，安装 R 包，如果您具有这些权限，以及如果是使用机器学习作业的服务器的唯一人员。

但是，如果你需要包与他人共享，或如果多个用户需要在服务器上运行机器学习作业，会设置共享的包库更高效。 SQL Server 支持此功能通过数据库角色。

数据库管理员负责设置角色并将用户添加到角色。 通过角色，数据库管理员可以控制谁有权添加或删除从 SQL Server 环境中，R 包，并可以审核包安装。

**用于程序包管理的数据库角色**


以下新的数据库角色在 SQL Server 中支持安全的安装和 R 包管理：

- `rpkgs-users`： 允许用户使用安装的成员的任何共享的包`rpkgs-shared`角色。

- `rpkgs-private`： 提供对共享的包的访问相同的权限`rpkgs-users`角色。 此角色的成员还可以安装、删除和使用个人作用域包。

-  `rpkgs-shared`： 提供相同的权限`rpkgs-private`角色。 属于此角色成员的用户还可以安装或删除共享包。

- `db_owner`： 具有相同的权限`rpkgs-shared`角色。 也可向用户授予安装或删除共享和专用包的权限。

**创建使用 T-SQL 的外部包库**


此外，SQL Server 2017 支持 T-SQL 语句，**创建外部库**，以支持由数据库管理员管理的外部库。 当前此语句可用于为。 其他支持计划在将来的 Python 包和为执行编写在其他平台，如 Linux 上的包中创建基于 Windows 的库。



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-set-up-sql-server-machine-learning-services-in-databaserset-up-sql-server-r-services-in-databasemd"></a>8.&nbsp;[设置 SQL Server 计算机学习 Services （数据库）](r/set-up-sql-server-r-services-in-database.md)

*更新时间： 2017年-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_7) | [下一步](#TitleNum_9))

<!-- Source markdown line 240.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 452dc36b4d0097f9562642238ba49eea0373d25b 4d355f6494b417dd90dce3943e7176eaece7336e  (PR=3070  ,  Filename=set-up-sql-server-r-services-in-database.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=0b832a9306244210e693bde7c476269455e9b6d8) -->



如果你的数据科学客户端计算机上创建 R 解决方案，并且需要通过使用 SQL Server 计算机作为计算上下文来运行代码，你可以使用 SQL 登录名或集成的 Windows 身份验证。

* 对于 SQL 登录名：确保该登录名对要读取数据的数据库拥有相应的权限。 你可以通过添加实现*连接到*和*选择*权限，或通过添加登录到*db_datareader*角色。 对于需要创建对象的登录名，添加*DDL_admin*权限。 必须将数据保存到表的登录名添加到的登录名为*db_datawriter*角色。

* 对于 Windows 身份验证： 你可能需要指定实例名称和其他连接信息的数据科学客户端上配置 ODBC 数据源。 有关详细信息，请参阅[ODBC 数据源管理器](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)。

**后续步骤**


验证脚本执行功能，在 SQL Server 中工作后，你可以从 SQL Server Management Studio、 Visual Studio 代码或可以向服务器发送的 T-SQL 语句的任何其他客户端运行 R 和 Python 的命令。

但是，你可能想要对系统配置，以支持使用大量的机器学习中，或添加新的 R 包进行一些更改。

本部分列出了你可以以支持机器学习一些常见修改。

**添加更多的工作帐户**


如果您认为可能很大程度，使用 R，或者如果希望多个用户同时处于正在运行的脚本，则可以增加分配给快速启动板服务的工作帐户数。 有关详细信息，请参阅 [修改用户帐户池的 SQL Server R Services--modify-the-user-account-pool-for-sql-server-r-services.md）。

**<a name="bkmk_optimize"></a>优化外部脚本执行的服务器**




&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-sql-server-configuration-for-use-with-rrsql-server-configuration-r-servicesmd"></a>9.&nbsp;[与 R 一起使用的 SQL Server 配置](r/sql-server-configuration-r-services.md)

*更新时间： 2017年-07-27* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_8) | [下一步](#TitleNum_10))

<!-- Source markdown line 149.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3f57bae70e3c118c1e2bcd57017322940bae83f8 f296242d470db47077cba4215ef420bd0c60bf33  (PR=2660  ,  Filename=sql-server-configuration-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=70a1fd4dbec68d22187585de69a1d603c39e259e) -->



如果查询返回单个内存节点 （节点 0），则你还没有硬件 NUMA，或硬件配置为交错 (非 NUMA)。 SQL Server 还会忽略硬件 NUMA 时有四个或更少的 Cpu，或者如果至少一个节点拥有，只有一个 CPU。

如果你的计算机有多个处理器，但没有硬件 NUMA，也可以使用[SOFT-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)若要将 Cpu 细分为较小的组。  在 SQL Server 2016 和 SQL Server 自 2017 年中，启动 SQL Server 服务时，将自动启用软件 NUMA 功能。

SQL Server 启用 SOFT-NUMA 后，为你; 的节点自动管理但是，若要针对特定工作负荷进行优化，可以禁用_软关联_和手动配置 CPU 相关性，软的 NUMA 节点。 尤其是当你使用的版本的支持资源调控的 SQL Server，这可以为你提供更好地控制对其工作负荷分配到的节点。 通过指定 CPU 关联并对齐具有的 Cpu 的组的资源池，你可以减少延迟，并确保相关的进程在同一个 NUMA 节点内执行。

配置 SOFT-NUMA 和 CPU 相关性以支持 R 工作负荷的整个过程如下所示：

1. 如果可用，请启用软件 NUMA
2. 定义处理器关联
3. 创建资源池以外部进程，使用 [资源调控器-.../r/resource-governance-for-r-services.md)
4. 将这些 [工作负荷组...-分配/../ relational-databases/resource-governor/resource-governor-workload-group.md） 到特定的地缘组

有关详细信息，包括示例代码，请参阅本教程： [SQL 优化提示和技巧 (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**其他资源：**



&nbsp;

&nbsp;

---

<a name="TitleNum_10"/>

### <a name="10-nbsp-performance-tuning-for-r-in-sql-serverrsql-server-r-services-performance-tuningmd"></a>10.&nbsp;[的 SQL Server 中的 R 性能调整](r/sql-server-r-services-performance-tuning.md)

*更新时间： 2017年-07-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_9) | [下一步](#TitleNum_11))

<!-- Source markdown line 76.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9c30753efdec81e499d5654b5b7a07f0cfe5b003 136a9f483bc8c9e1f69cf9d340d1472c21a52ec4  (PR=2565  ,  Filename=sql-server-r-services-performance-tuning.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=cf8509cab2424529ca0ed16c936fa63a139dfca4) -->



- 配置 SQL Server 实例以平衡数据库引擎操作和 R 或 Python 脚本在适当的级别执行。 这可能包括更改内存和 CPU 使用情况、 NUMA 和处理器关联设置，并且创建资源组的 SQL Server 默认值。

- 优化支持高效使用的外部脚本的服务器计算机。 这可以包括增加用于外部脚本执行，启用包管理的帐户的数量和分配用户相关的安全角色。

- 将特定的优化应用到数据存储和 SQL Server，包括索引和统计信息策略、 查询设计和查询优化和用于机器学习的表的设计中的传输。 您还可以分析数据源和数据传输方法，或修改 ETL 过程，以便优化提取特征。

- 优化分析的模型，以避免导致效率较低。 可能的优化的作用域取决于的 R 代码的包和你使用的数据的复杂性。 关键任务包括消除代价高昂的数据转换或数据准备工作或功能工程将任务卸载从 R 或 Python 到 ETL 过程或 SQL。 你可能重构脚本、 消除串联包安装，将 R 代码划分为训练、 评分，和评估，单独的过程或简化代码，以作为存储过程更有效地工作。

**本系列文章**


+ [性能优化的 SQL Server 的硬件--中的 R...\r\sql-server-configuration-r-services.md)

    提供配置硬件的指南，..！包括 NotShown-ssNoVersion_md...\..\includes\ssnoversion-md.md)]已安装，以及用于配置要更好地支持外部脚本的 SQL Server 实例。 它很适合用于**数据库管理员**。

+ [SQL Server 中的 R 性能优化的代码和数据优化...\r\r-and-data-optimization-r-services.md)



&nbsp;

&nbsp;

---

<a name="TitleNum_11"/>

### <a name="11-nbsp-data-science-scenarios-and-solution-templatestutorialsdata-science-scenarios-and-solution-templatesmd"></a>11.&nbsp;[数据科学方案和解决方案模板](tutorials/data-science-scenarios-and-solution-templates.md)

*更新时间： 自 2017 年-08-28* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_10) | [下一步](#TitleNum_12))

<!-- Source markdown line 45.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 22c621731015f2192cb0b8d61b22062a4be50e70 6cf9e3f0a3803ed2bce9c4ffadfd7314f15f6b51  (PR=2964  ,  Filename=data-science-scenarios-and-solution-templates.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=7b4f037616e0559ac62bbae5dbe04aeffe529b06) -->



[预测何时以及如何联系主管](https://microsoft.github.io/r-server-campaign-optimization/)

**新增功能：**此解决方案使用保险行业数据来预测基于人口统计信息、 历史响应数据和特定于产品的详细信息的主管。  建议还会生成以指示最佳的通道和向方法用户影响购买行为的时间。

**如何：**解决方案创建，并将多个模型进行比较。 自动化的数据集成和使用存储的过程的数据准备，还演示了解决方案。 为 SQL Server 数据库中，在 Azure 和 HDInsight Spark 提供了并行示例。

**卫生保健： 预测医院保持状态的长度**


[预测医院保持状态的长度](https://gallery.cortanaintelligence.com/Solution/Predicting-Length-of-Stay-in-Hospitals-1)

**新增功能：**准确预测哪些患者可能需要长期医疗是保健和规划的一个重要部分。 管理员需要能够确定哪些功能需要更多资源，并且医护人员想要确保它们可以满足患者的需求。

**如何：**此解决方案使用数据科学虚拟机，并且与启用的机器学习中包括的 SQL Server 实例。 它还包括一组可用于与已部署的模型进行交互的 Power BI 报表。

**客户改动**


[客户改动预测模板 (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)

**新增功能：**分析和预测客户改动率很重要中必须管理和阻止的客户将你的竞争对手丢失任何行业： 银行、 电信和零售，仅举几例。 流失分析的目的是确认哪些客户可能会流失，然后采取适当措施维系这些客户及其业务。



&nbsp;

&nbsp;

---

<a name="TitleNum_12"/>

### <a name="12-nbsp-whats-new-in-machine-learning-services-in-sql-serverwhat-s-new-in-sql-server-machine-learning-servicesmd"></a>12.&nbsp;[什么是 SQL Server 中的机器学习服务中的新增功能](what-s-new-in-sql-server-machine-learning-services.md)

*更新时间： 自 2017 年-08-02* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([以前](#TitleNum_11))

<!-- Source markdown line 33.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 025e68a93895a3788a63847cd91bff068775acf3 6dc0be2920c670235038a126d135e08d6f16ec3a  (PR=2712  ,  Filename=what-s-new-in-sql-server-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\  ,  MergeCommitSha40=ea75391663eb4d509c10fb785fcf321558ff0b6e) -->



> 在 Linux 上，或在 Azure SQL 数据库中运行 SQL Server 时，机器学习服务，包括使用 R 或 Python，当前不支持。 寻找更高版本中的更改。
>
> 但是，使用预测函数的本机评分是目前支持的 Linux 版本。

**数据库 Python 集成**


可以在存储过程中运行 Python，也可以执行 Python 远程作为计算上下文中使用 SQL Server 计算机。 此集成将打开新的 Python 开发人员和数据科学家使用的 SQL Server 功能，例如从 Microsoft 浏览创新 vast 社区途径**revoscalepy**和**microsoftml**.

SQL Server 开发人员访问到广泛的 Python 库从开放源生态系统，包括如 scikit 常用框架的了解，Tensorflow、 Caffe 和 Theano/Keras。

但运行的 Python 数据库中不只是为了机器学习;有大量的集成与 SQL，利用要提供更智能、 功能强大的解决方案的相应语言的优势的 Python 其他潜在应用程序。

+ **revoscalepy**

    此版本包括的最终版本**revoscalepy**，其中提供的可缩放的 Pythonic 等效流式处理中 RevoScaleR 的算法。 你可以创建用于线性和逻辑回归、 决策树，提升的树和随机林，所有可并行化，并且能够在远程计算上下文中运行的 Python 模型。

    有关详细信息，请参阅 [什么是 revoscalepy-python/模拟-是-revoscalepy.md）。

+ Python 远程计算上下文

    此版本支持使用多个数据源和远程计算上下文。 在远程 SQL 服务器上，若要浏览数据或生成模型，而无需移动数据，数据科研人员或开发人员可以执行 Python 代码。 使用远程计算上下文要求**revoscalepy**。







## <a name="similar-articles"></a>类似文章

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

本部分列出了一些非常类似文章中我们公共 GitHub.com 存储库中的其他主题区域的最近更新项目： [MicrosoftDocs/sql 文档](https://github.com/MicrosoftDocs/sql-docs/)。

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新 + 更新 (3 + 12): **sql 高级分析**文档](../advanced-analytics/new-updated-advanced-analytics.md)
- [新 + 更新 (5 + 0):**连接到 SQL**文档](../connect/new-updated-connect.md)
- [新 + 更新 (5 + 1): **sql 数据库引擎**文档](../database-engine/new-updated-database-engine.md)
- [新 + 更新 (19 + 82): **sql Integration Services**文档](../integration-services/new-updated-integration-services.md)
- [新 + 更新 (1 + 8): **sql Linux**文档](../linux/new-updated-linux.md)
- [新 + 更新 (12 + 1): **sql 的关系数据库**文档](../relational-databases/new-updated-relational-databases.md)
- [新 + 更新 (0 + 1): **sql Reporting Services**文档](../reporting-services/new-updated-reporting-services.md)
- [新 + 更新 (7 + 1): **Microsoft SQL Server**文档](../sql-server/new-updated-sql-server.md)
- [新 + 更新 (1 + 1): **SQL Server Data Tools (SSDT)**文档](../ssdt/new-updated-ssdt.md)
- [新 + 更新 (0 + 2): **SQL Server 迁移助手 (SSMA)**文档](../ssma/new-updated-ssma.md)
- [新 + 更新 (1 + 4): **SQL Server Management Studio (SSMS)**文档](../ssms/new-updated-ssms.md)
- [新 + 更新 (4 + 1): **TRANSACT-SQL**文档](../t-sql/new-updated-t-sql.md)
- [新 + 更新 (0 + 1): **SQL 的工具**文档](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>没有新的或最近更新文章的主题区域

- [新的和更新的文章 (0+0)：ActiveX Data Objects (ADO) for SQL 文档](../ado/new-updated-ado.md)
- [新 + 更新 (0 + 0): **Analysis Services for SQL**文档](../analysis-services/new-updated-analysis-services.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新 + 更新 (0 + 0): **sql 的 Master Data Services (MDS)**文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../sample/new-updated-sample.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)



