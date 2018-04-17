---
title: 将 R 代码，以用在 SQL Server 机器学习服务转换 |Microsoft 文档"
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: bf3d272bd4b5c1227aa8a1969727ea17f5b65596
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>将转换为在 SQL Server （数据库） 实例中执行的 R 代码
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供有关如何修改 R 代码，以使用 SQL Server 中的深入指导。 

将 R 代码从 R Studio 或另一个环境移动到 SQL Server 中，文件时最常代码在运行无需进一步修改： 例如，如果代码是简单的如需要一段时间的函数输入，并返回一个值。 它也是易于使用的端口解决方案**RevoScaleR**或**MicrosoftML**支持在不同的执行上下文中进行少量的更改执行的包。

但是，你的代码可能需要重大更改，如果任何适用以下原则：

+ 使用 R 库访问网络或无法在 SQL Server 上安装的。
+ 代码使单独调用外部 SQL Server，如 Excel 工作表、 共享上的文件和其他数据库的数据源。 
+ 你想要运行中的代码*@script*参数[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)和也参数化存储的过程。
+ 您的原始解决方案包括多个步骤，可能会在生产环境中执行独立，如数据准备或与模型训练、 评分，或报告的特征工程如果更加高效。
+ 你想要提高通过更改库，使用并行执行，或卸载到 SQL Server 的某些处理优化性能。 

## <a name="step-1-plan-requirements-and-resources"></a>步骤 1. 计划要求和资源

**包**

+ 确定需要哪些包，并确保它们在 SQL Server 上工作。
 
+ 机器学习服务使用的默认包库中，请提前安装包。 不支持用户库。

**数据源** 

+ 如果你想要将在你 R 代码嵌入[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，标识主要和辅助数据源。 

    + **主**数据源是大型数据集，如模型定型数据或预测的输入的数据。 计划将你最大的数据集映射到的输入参数[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

    + **辅助**数据源是通常较小的数据集，如因素或其他分组变量的列表。 
    
    目前，sp_execute_external_script 支持单个数据集作为存储过程的输入。 但是，你可以添加多个标量或 binary 输入。

    通过执行前面的存储的过程调用不能用作输入到[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 你可以使用查询、 视图或其他任何有效的 SELECT 语句。

+ 确定所需的输出。 如果你运行使用 sp_execute_external_script 的 R 代码，该存储的过程可以作为结果输出只在一个数据帧。 但是，你还可以输出多个标量输出，包括图形，并源自 R 代码或 SQL 参数中的二进制格式，以及其他标量值的模型。

**数据类型**

+ 针对可能的数据类型问题创建一份查检表。

    SQL Server 机器学习服务支持所有 R 数据类型。 但是，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持的更广泛的数据类型不是因此，某些隐式数据类型转换时，将执行发送[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据到 R，反之亦然。 你可能需要显式强制转换或将某些数据转换。 

    支持 NULL 值。 但是，R 使用`na`数据构造来表示缺失值，这类似于 null。

+ 请考虑删除依赖于不能使用的： 例如，rowid 数据和从 SQL Server 的 GUID 数据类型不能供 R 和生成错误。

    有关详细信息，请参阅[R 库和数据类型](../r/r-libraries-and-data-types.md)。

## <a name="step-2-convert-or-repackage-code"></a>步骤 2. 将转换或重新打包代码

你更改代码的量取决于是否想要提交的 R 代码从远程客户端运行在 SQL Server 计算上下文中，或想要将代码部署可以提供更好的性能和数据安全的存储过程的一部分。 在存储过程中包装你的代码有一定满足一些附加要求。 

+ 为 SQL 查询定义主输入的数据，只要有可能，以避免数据移动。

+ 在运行时 R 存储过程，你可以通过多个**标量**输入。 对于你想要在输出中使用任何参数，添加**输出**关键字。 

    例如，以下标量输入`@model_name`包含的模型名称，这也是在其自己的列在结果中的输出：

    ```SQL
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ 你在将作为参数传递存储任何的过程变量[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)必须映射到中的 R 代码的变量。 默认情况下，变量按名称映射。

    输入数据集中的所有列必须还都映射到 R 脚本中的变量中。  例如，假定你的 R 脚本包含一个公式如下所示：

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    如果输入数据集不包含具有匹配名称 ArrDelay、 CRSDepTime、 DayOfWeek、 CRSDepHour 和 DayOfWeek 的列，则会引发错误。

+ 在某些情况下，输出架构必须针对为结果提前定义。

    例如，若要将数据插入到表，必须使用**与结果集**子句以指定的架构。

    如果 R 脚本使用的自变量，可能也是必需的输出架构`@parallel=1`。 原因是 SQL Server 可能会创建多个进程来并行运行查询，最后收集结果。 因此，可以创建并行进程之前，必须准备的输出架构。
    
    在其他情况下，也可以通过使用选项中省略结果架构**与结果集未定义**。 此语句从 R 脚本中返回数据集，而无需命名列或指定的 SQL 数据类型。

+ 请考虑生成计时或跟踪数据使用 T-SQL 的而不是。

    例如，你可以将系统时间或用于审核和存储添加到结果中，通过传递的 T-SQL 的调用，而不是在 R 脚本中生成类似数据的其他信息。 

**提高性能和安全性**

+ 要避免编写预测或中间结果文件。 预测向表写入相反，以避免数据移动。

+ 提前，运行所有查询以及查看 SQL Server 查询计划，以确定可以并行执行的任务。

    如果输入的查询可以并行化，设置`@parallel=1`到你 arguments 的一部分[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 

    只要 SQL Server 可以处理分区表或者在多个进程之间分布查询并最终聚合结果，就通常可以使用此标志进行并行处理。 如果用于训练模型的算法需要读取所有数据，或者你需要创建聚合，则通常无法使用此标志进行并行处理。

+ 检查 R 代码，确定是否可以独立执行某些步骤，或者可以使用单独的存储过程调用来更有效地执行某些步骤。 例如，你可能会通过分别执行特征工程或提取特征，并将值保存到表获得更好的性能。

+ 查找有关如何使用基于集的计算 T-SQL 的而不是 R 代码。

    例如，本 R 解决方案演示了如何用户定义 T-SQL 的函数和 R 可以执行相同的功能工程任务：[数据科学端到端演练](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)。

+ 如果可能，将使用的传统 R 函数**ScaleR**支持分布式的执行的函数。 有关详细信息，请参阅[比较的基础 R 和缩放 R 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)。

+ 咨询数据库开发人员来确定如何通过使用 SQL Server 功能，如提高性能[内存优化表](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)，或者，如果你具有企业版[资源调控器](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor))。

    有关详细信息，请参阅[分析服务的 SQL Server 优化提示和技巧](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>步骤 3. 准备部署

+ 通知管理员，以便在部署代码之前可以安装和测试包。 

    在开发环境中，则可能是可以将程序包安装为属于你的代码，但这是不好的做法在生产环境中。 

    用户库不支持，无论你是要使用存储的过程，还是要在 SQL Server 计算上下文中运行 R 代码。

**包中的存储过程的 R 代码**

+ 如果代码是相对简单，你可以将其嵌入 T-SQL 的用户定义函数而不进行修改中,，这些示例中所述：

    + [创建在 rxExec 中运行的 R 函数](..\tutorials\deepdive-create-a-simple-simulation.md)
    + [使用 T-SQL 和 R 的特征工程](..\tutorials\sqldev-create-data-features-using-t-sql.md)

+ 如果更复杂的代码，则使用 R 包**sqlrutils**要转换你的代码。 此包旨在帮助编写良好的存储的过程代码的有经验的 R 用户。 

    第一步是重写 R 代码，作为单个函数具有明确定义的输入和输出。

    然后，使用**sqlrutils**包以正确的格式生成的输入和输出。 **Sqlrutils**包为你生成的完整存储的过程代码和还可以在数据库中注册该存储的过程。 

    有关详细信息和示例，请参阅[SqlRUtils](../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)。

**与其他工作流集成**

+ 利用 T-SQL 的工具和 ETL 过程。 执行特征工程、 功能提取和数据清理提前数据工作流的一部分。

    当你使用在专用的 R 开发环境中如[!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)]或 RStudio，你可能到你的计算机中提取数据、 分析数据以迭代方式，然后写出或显示的结果。 
    
    但是，当独立 R 代码迁移到 SQL Server 中，此过程的大部分可简化或委派给其他 SQL Server 工具。 

+ 使用安全、 异步可视化效果策略。

    SQL Server 的用户通常无法访问在服务器上，文件和 SQL 客户端工具通常不支持 R 图形设备。 如果你生成图形或其他图形作为解决方案的一部分，请考虑为二进制数据导出绘图和保存到表，或者通过编写。

+ 由应用程序，可以将预测和计分函数包装在直接访问的存储过程。

### <a name="other-resources"></a>其他资源

若要查看如何在 SQL Server 中部署 R 解决方案的示例，请参阅这些示例：

+ [生成 ski 租赁业务使用 R 和 SQL Server 的预测模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [SQL 开发人员的数据库中分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)演示如何你可以通过提高了 R 代码更加模块化包装存储过程中

+ [端到端数据科学解决方案](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)R 和 T-SQL 中包括的特征工程比较
