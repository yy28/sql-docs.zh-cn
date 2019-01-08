---
title: 转换 R 代码的存储过程的 SQL Server 机器学习服务
description: 将 R 代码迁移到 SQL 服务器上的关系数据的解决方案部署和数据访问的 SQL Server 存储过程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: fd3197fa542a6650d482f7c6019ad9e8b1f2c7c0
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2018
ms.locfileid: "53644996"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>将 SQL Server （数据库内） 实例中执行的 R 代码转换
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文提供有关如何修改 R 代码以使用 SQL Server 中的高级指导。 

当将 R 代码从 R Studio 或另一个环境移到 SQL Server 中时，最常代码在运行无需进一步修改： 例如，如果代码非常简单，如需要一段时间的函数输入，并返回一个值。 它也是易于使用的端口解决方案**RevoScaleR**或**MicrosoftML**支持在进行少量的更改不同的执行上下文中执行的包。

但是，你的代码可能需要重大更改，如果任何满足以下条件：

+ 使用访问网络或不能在 SQL Server 上安装的 R 库。
+ 代码会单独调用外部 SQL Server，如 Excel 工作表、 文件共享上和其他数据库的数据源。 
+ 你想要运行中的代码*@script*参数[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)和也参数化存储的过程。
+ 您的原始解决方案包括可能会在生产环境中执行独立，如数据准备或与模型定型、 评分、 或报告的功能设计更加高效的多个步骤。
+ 你想要提高通过更改库、 使用并行执行，或卸载到 SQL Server 的一些处理来优化性能。 

## <a name="step-1-plan-requirements-and-resources"></a>步骤 1. 计划要求和资源

**包**

+ 确定所需的程序包，并确保它们能在 SQL Server 上。
 
+ 使用机器学习服务的默认包库中，请提前安装包。 不支持用户库。

**数据源** 

+ 如果你想要在 R 代码中的嵌入[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，标识的主要和辅助数据源。 

    + **主**数据源是大型数据集，例如模型训练数据或用于预测的输入的数据。 计划将你最大的数据集映射到的输入参数[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

    + **辅助**数据源是通常较小的数据集，如因素或附加分组变量的列表。 
    
    目前，sp_execute_external_script 支持单个数据集作为存储过程的输入。 但是，可以添加多个标量或二进制输入。

    前面带有 EXECUTE 的存储的过程调用不能用作对的输入[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 可以使用查询、 视图或其他任何有效的 SELECT 语句。

+ 确定所需的输出。 运行使用 sp_execute_external_script 的 R 代码，如果存储的过程可以将结果输出只是一个数据帧。 但是，也可以输出多个标量输出，包括图形和二进制格式，以及其他标量值中的模型派生自 R 代码或 SQL 参数。

**数据类型**

+ 针对可能的数据类型问题创建一份查检表。

    SQL Server 机器学习服务支持所有 R 数据类型。 但是，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持更大的不同数据类型比。因此，执行某些隐式数据类型转换时发送[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据到 R，反之亦然。 您可能需要显式强制转换或转换某些数据。 

    支持 NULL 值。 但是，R 使用`na`数据构造来表示缺失值，这类似于 null 值。

+ 请考虑消除： 例如，rowid 不能使用的数据和 GUID 数据类型从 SQL Server 无法使用 R 并生成错误的依赖关系。

    有关详细信息，请参阅[R 库和数据类型](../r/r-libraries-and-data-types.md)。

## <a name="step-2-convert-or-repackage-code"></a>步骤 2. 将转换或重新打包的代码

更改代码的多少取决于是否想要提交的 R 代码从远程客户端运行在 SQL Server 计算上下文中，或想要将代码部署可以提供更好的性能和数据安全的存储过程的一部分。 在存储过程中包装您的代码强加一些额外要求。 

+ 为 SQL 查询定义主输入的数据，只要有可能，以避免数据移动。

+ 当存储过程中运行 R，可以通过多个**标量**输入。 你想要在输出中使用任何参数，将添加**输出**关键字。 

    例如，下面的标量输入`@model_name`包含模型名称，也是其各自的结果中的列中的输出：

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ 作为存储过程的参数中传递的任何变量[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)必须映射到 R 代码中的变量。 默认情况下，变量按名称映射。

    输入数据集中的所有列也必须都映射到 R 脚本中的变量。  例如，假设 R 脚本中包含类似如下的公式：

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    如果输入数据集不包含具有匹配名称 ArrDelay、 CRSDepTime、 DayOfWeek、 CRSDepHour 和 DayOfWeek 的列，则会引发错误。

+ 在某些情况下，必须提前为结果地定义输出架构。

    例如，若要将数据插入到表，必须使用**结果集与**子句来指定的架构。

    如果 R 脚本使用参数，输出架构也是必需`@parallel=1`。 原因是 SQL Server 可能会创建多个进程来并行运行查询，最后收集结果。 因此，可以创建并行进程之前，必须准备的输出架构。
    
    在其他情况下，可以通过使用选项忽略结果架构**与 RESULT SETS UNDEFINED**。 此语句从 R 脚本中返回数据集，而无需命名列或指定的 SQL 数据类型。

+ 请考虑生成计时或跟踪数据使用 T-SQL 而不是。

    例如，可以传递系统时间或用于审核和存储添加到结果，传递的 T-SQL 的调用，而不是在 R 脚本中生成类似的数据的其他信息。 

**提高性能和安全性**

+ 避免编写预测或中间结果保存到文件。 预测到的表改为编写，以避免数据移动。

+ 提前运行所有查询并查看 SQL Server 查询计划，以确定可并行执行的任务。

    如果输入的查询可并行化，设置`@parallel=1`作为你的参数的一部分[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 

    只要 SQL Server 可以处理分区表或者在多个进程之间分布查询并最终聚合结果，就通常可以使用此标志进行并行处理。 如果用于训练模型的算法需要读取所有数据，或者你需要创建聚合，则通常无法使用此标志进行并行处理。

+ 检查 R 代码，确定是否可以独立执行某些步骤，或者可以使用单独的存储过程调用来更有效地执行某些步骤。 例如，可能会通过单独执行特征工程或特征提取，并将值保存到表来获得更好的性能。

+ 查找使用 T-SQL 而不是 R 代码的基于集的计算方式。

    例如，此 R 解决方案显示了如何用户定义 T-SQL 函数以及 R 可执行相同的特征工程任务：[数据科学端到端演练](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)。

+ 如果可能，将为与传统的 R 函数**ScaleR**支持分布式的执行函数。 有关详细信息，请参阅[比较的基础 R 和 Scale R 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r)。

+ 数据库开发人员确定如何通过使用类似于 SQL Server 功能来提高性能，请咨询[内存优化表](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)，或者，如果拥有 Enterprise Edition[资源调控器](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor))。

    有关详细信息，请参阅[分析服务的 SQL Server 优化提示和技巧](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>步骤 3. 为部署做准备

+ 通知管理员，以便在部署代码之前可以安装和测试包。 

    在开发环境中，也许可以将它作为你的代码的一部分安装包，但这是在生产环境中一次不良实践。 

    用户库不支持，无论您是使用存储的过程或 SQL Server 计算上下文中运行 R 代码。

**包中的存储过程的 R 代码**

+ 如果你的代码相对简单，如这些示例中所述可以将它嵌入 T-SQL 用户定义函数而无需修改中,：

    + [创建在 rxExec 中运行的 R 函数](../tutorials/deepdive-create-a-simple-simulation.md)
    + [使用 T-SQL 和 R 的功能设计](../tutorials/sqldev-create-data-features-using-t-sql.md)

+ 如果代码更复杂，请使用 R 包**sqlrutils**以转换您的代码。 此包用于帮助有经验的 R 用户编写良好的存储的过程代码。 

    第一步是作为单个明确定义的输入和输出函数重写 R 代码。

    然后，使用**sqlrutils**包以正确的格式生成的输入和输出。 **Sqlrutils**包，生成完整的存储的过程代码，并还可以在数据库中注册该存储的过程。 

    有关详细信息和示例，请参阅[sqlrutils (SQL)](ref-r-sqlrutils.md)。

**与其他工作流集成**

+ 利用 T-SQL 的工具和 ETL 进程。 执行特征工程、 特征提取和数据清理预先数据工作流的一部分。

    工作时在专用的 R 开发环境中如[!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)]或 RStudio 中，您可能会提取到计算机的数据、 分析数据以迭代方式，然后写出或显示结果。 
    
    但是，在独立的 R 代码迁移到 SQL Server，此过程的大部分可以简化或委派给其他 SQL Server 工具。 

+ 使用安全、 异步可视化策略。

    SQL Server 的用户通常无法访问服务器上的文件和 SQL 客户端工具通常不支持 R 图形设备。 如果您生成绘图或其他图形作为解决方案的一部分，请考虑将绘图作为二进制数据导出和保存到表，或写入。

+ 通过应用程序包装预测评分函数用于直接访问的存储过程中。

### <a name="other-resources"></a>其他资源

若要查看如何在 SQL Server 中部署 R 解决方案的示例，请参阅这些示例：

+ [生成雪橇租赁公司使用 R 和 SQL Server 的预测模型](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [SQL 开发人员的数据库内分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)演示了如何使在 R 代码更加模块化通过将其包装在存储过程

+ [端到端数据科学解决方案](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)R 和 T-SQL 中包括特征工程的比较
