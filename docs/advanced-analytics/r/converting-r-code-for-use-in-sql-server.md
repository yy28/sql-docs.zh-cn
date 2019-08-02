---
title: 转换存储过程的 R 代码
description: 将 R 代码迁移到用于解决方案部署的 SQL Server 存储过程, 并对 SQL Server 上的关系数据进行数据访问。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 536be600d319335173dbf112ec2d8f67cc7bf14b
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715740"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>转换 R 代码以在 SQL Server (数据库内) 实例中执行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文提供了有关如何修改 R 代码以在 SQL Server 中工作的高级指南。 

将 R 代码从 R Studio 或另一环境移到 SQL Server 时, 大多数情况下, 代码不会进行进一步修改: 例如, 如果代码很简单, 例如, 采用某些输入并返回值的函数。 此外, 还可以更轻松地移植使用**RevoScaleR**或**MicrosoftML**包的解决方案, 这些包支持在具有最小更改的不同执行上下文中执行。

但是, 如果满足以下任一条件, 你的代码可能需要进行重大更改:

+ 可以使用访问网络或无法在 SQL Server 上安装的 R 库。
+ 此代码对 SQL Server 之外的数据源进行单独调用, 如 Excel 工作表、共享上的文件和其他数据库。 
+ 需要在 *@script* [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)的参数中运行代码, 并将该存储过程参数化。
+ 最初的解决方案包含多个步骤, 如果在生产环境中单独执行这些步骤, 则这些步骤可能更高效, 如数据准备、功能设计与模型定型、评分或报告。
+ 需要通过更改库、使用并行执行或将某些处理卸载到 SQL Server 来提高优化性能。 

## <a name="step-1-plan-requirements-and-resources"></a>步骤 1. 规划要求和资源

**包**

+ 确定所需的包, 并确保它们处理 SQL Server。
 
+ 预先在机器学习服务使用的默认包库中安装包。 不支持用户库。

**数据源** 

+ 如果打算在[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)中嵌入 R 代码, 请标识主数据源和辅助数据源。 

    + **主**数据源是大型数据集, 例如模型定型数据或用于预测的输入数据。 计划将最大的数据集映射到[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)的输入参数。

    + **辅助**数据源通常是较小的数据集, 例如因素列表或其他分组变量。 
    
    目前, sp_execute_external_script 仅支持单个数据集作为存储过程的输入。 但是, 可以添加多个标量或二进制输入。

    前面带有 EXECUTE 的存储过程调用不能用作[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)的输入。 您可以使用查询、视图或任何其他有效的 SELECT 语句。

+ 确定所需的输出。 如果使用 sp_execute_external_script 运行 R 代码, 则该存储过程只会输出一个数据帧。 但是, 还可以输出多个标量输出, 包括二进制格式的图形和模型, 以及从 R 代码或 SQL 参数派生的其他标量值。

**数据类型**

+ 针对可能的数据类型问题创建一份查检表。

    SQL Server 机器学习服务支持所有 R 数据类型。 但是, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持的数据类型比 R 更多。因此, 在将数据发送[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]到 R 时, 会执行某些隐式数据类型转换, 反之亦然。 可能需要显式转换或转换某些数据。 

    支持 NULL 值。 但是, R 使用`na`数据构造来表示缺失值, 这类似于 null。

+ 请考虑消除对 R 不能使用的数据的依赖关系例如, 来自 SQL Server 的 rowid 和 GUID 数据类型不能由 R 使用并生成错误。

    有关详细信息, 请参阅[R 库和数据类型](../r/r-libraries-and-data-types.md)。

## <a name="step-2-convert-or-repackage-code"></a>步骤 2. 转换或重新打包代码

更改代码的方式取决于您是要从远程客户端提交 R 代码以在 SQL Server 计算上下文中运行, 还是要将代码部署为存储过程的一部分, 从而提供更好的性能和数据安全。 将代码包装在存储过程中有一些额外的要求。 

+ 尽可能将主要输入数据定义为 SQL 查询, 以避免数据移动。

+ 当在存储过程中运行 R 时, 可以通过多个**标量**输入。 对于要在输出中使用的任何参数, 请添加**output**关键字。 

    例如, 下面的标量输入`@model_name`包含模型名称, 该名称也会在结果中其自身的列中输出:

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ 作为存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)的参数传入的任何变量必须映射到 R 代码中的变量。 默认情况下，变量按名称映射。

    输入数据集中的所有列也必须映射到 R 脚本中的变量。  例如, 假设 R 脚本包含如下公式:

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    如果输入数据集不包含具有匹配名称 ArrDelay、CRSDepTime、DayOfWeek、了基于和 DayOfWeek 的列, 则会引发错误。

+ 在某些情况下, 必须提前为结果定义输出架构。

    例如, 若要将数据插入表中, 您必须使用**WITH RESULT SET**子句来指定架构。

    如果 R 脚本使用参数`@parallel=1`, 则还需要输出架构。 原因是 SQL Server 可能会创建多个进程来并行运行查询，最后收集结果。 因此, 必须先准备好输出架构, 然后才能创建并行进程。
    
    在其他情况下, 您可以通过使用**带有未定义结果集**的选项来省略结果架构。 此语句返回 R 脚本中的数据集, 而无需命名列或指定 SQL 数据类型。

+ 请考虑使用 T-sql 而不是 R 生成计时或跟踪数据。

    例如, 你可以通过将传递给结果的 T-sql 调用 (而不是在 R 脚本中生成相似数据), 传递系统时间或用于审核和存储的其他信息。 

**提高性能和安全性**

+ 避免将预测或中间结果写入文件。 改为将预测写入表, 以避免数据移动。

+ 提前运行所有查询, 并查看 SQL Server 查询计划, 以确定可并行执行的任务。

    如果输入查询可并行化, 请将`@parallel=1`参数设置为[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)的一部分。 

    只要 SQL Server 可以处理分区表或者在多个进程之间分布查询并最终聚合结果，就通常可以使用此标志进行并行处理。 如果用于训练模型的算法需要读取所有数据，或者你需要创建聚合，则通常无法使用此标志进行并行处理。

+ 检查 R 代码，确定是否可以独立执行某些步骤，或者可以使用单独的存储过程调用来更有效地执行某些步骤。 例如, 您可以通过单独执行特征工程或特征提取, 并将值保存到表中来获得更好的性能。

+ 查找使用 T-sql 而不是 R 代码进行基于集的计算的方式。

    例如, 此 R 解决方案显示了用户定义的 T-sql 函数和 R 如何执行相同的功能工程任务:[数据科学端到端演练](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)。

+ 如果可能, 请将传统 R 函数替换为支持分布式执行的**ScaleR**函数。 有关详细信息, 请参阅[Base r 和 Scale r 函数的比较](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)。

+ 请咨询数据库开发人员, 了解如何使用[内存优化表](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)等 SQL Server 功能提高性能, 如果您有企业版, [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor))。

    有关详细信息, 请参阅[SQL Server 分析服务的优化提示和技巧](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>步骤 3. 准备部署

+ 通知管理员，以便在部署代码之前可以安装和测试包。 

    在开发环境中, 可以将包安装为代码的一部分, 但这在生产环境中是一种不好的做法。 

    无论是使用存储过程还是在 SQL Server 计算上下文中运行 R 代码, 都不支持用户库。

**在存储过程中将 R 代码打包**

+ 如果代码相对简单, 则可以在不进行修改的情况下将其嵌入 T-sql 用户定义函数中, 如以下示例中所述:

    + [创建在 rxExec 中运行的 R 函数](../tutorials/deepdive-create-a-simple-simulation.md)
    + [使用 T-sql 和 R 的功能设计](../tutorials/sqldev-create-data-features-using-t-sql.md)

+ 如果代码更复杂, 请使用 R 包**sqlrutils**转换代码。 此软件包旨在帮助有经验的 R 用户编写良好的存储过程代码。 

    第一步是将 R 代码重写为具有明确定义的输入和输出的单个函数。

    然后, 使用**sqlrutils**包生成正确格式的输入和输出。 **Sqlrutils**包会为您生成完整的存储过程代码, 还可以在数据库中注册该存储过程。 

    有关详细信息和示例, 请参阅[sqlrutils (SQL)](ref-r-sqlrutils.md)。

**与其他工作流集成**

+ 利用 T-sql 工具和 ETL 进程。 作为数据工作流的一部分, 预先执行特征工程、功能提取和数据清理。

    当你在专用的 R 开发环境 (如[!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)]或 RStudio) 中工作时, 你可以将数据提取到你的计算机上, 以迭代方式分析数据, 然后写出或显示结果。 
    
    但是, 在将独立 R 代码迁移到 SQL Server 时, 此过程的大部分内容可以简化或委托给其他 SQL Server 工具。 

+ 使用安全的异步可视化策略。

    SQL Server 用户通常无法访问服务器上的文件, 而 SQL 客户端工具通常不支持 R 图形设备。 如果生成图形或其他图形作为解决方案的一部分, 请考虑将绘图导出为二进制数据, 并将其保存到表或写入。

+ 将预测和评分函数包装在存储过程中, 以便应用程序直接访问。

### <a name="other-resources"></a>其他资源

若要查看如何在 SQL Server 中部署 R 解决方案的示例, 请参阅以下示例:

+ [使用 R 和 SQL Server 为 ski 租赁企业构建预测模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [适用于 SQL 开发人员的数据库内分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)演示如何通过将 R 代码包装在存储过程中, 使其更具模块化

+ [端到端数据科学解决方案](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)包括 R 和 T-sql 中的功能设计比较
