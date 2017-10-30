---
title: "转换 R 代码以便在 R Services 中使用 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 0b11ab52-b2f9-4a4f-b1ab-68ba09c8adcc
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ed5f9052467492fe4bbbfb4ac0682c08a7ba8062
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="converting-r-code-for-use-in-r-services"></a>转换 R 代码以便在 R Services 中使用

当你将 R 代码从 R Studio 或另一个环境移到 SQL Server 时，通常代码在运行无需进一步修改时添加到 *@script* 参数[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 如果您已开发你的解决方案使用尤其如此**RevoScaleR**函数，使其相对简单，若要更改执行上下文。

但是，通常我们想要修改 R 代码以便在 SQL Server 中运行，目的是利用与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的更紧密集成，同时避免产生不菲的数据传输费用。

若要查看有关如何在 SQL Server 中运行 R 代码的示例，请参阅以下演练：

+ [SQL 开发人员的数据库中分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)演示如何你可以通过提高了 R 代码更加模块化包装存储过程中

+ [端到端数据科学解决方案](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)R 和 T-SQL 中包括的特征工程比较

## <a name="how-the-data-science-process-changes-in-sql-server"></a>数据科学过程如何更改 SQL Server 中

当你使用在专用的 R 开发环境中如[!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)]或 RStudio、 典型的工作流是到你的计算机中提取数据、 分析数据以迭代方式，然后写出或显示的结果。 但是，当独立 R 代码迁移到 SQL Server 中，此过程的大部分可简化或委派给其他 SQL Server 工具。 此外，因此这样做可以提高在许多情况下的性能。

| 外部代码 | SQL Server 中的 R |
|-------|-------|
| 引入数据| 定义为 SQL 查询的输入的数据。 避免数据移动。 |
| 汇总和可视化数据| 图形可以导出为图像或发送到远程工作站。|
|特征工程| 如果你不想要更改你的代码，但查看优化你的查询，请使用 R 数据库中。 调查是否可能会更有效，以调用 T-SQL 的函数或自定义的 Udf。|
|分析过程的数据清理部分| 执行特征工程、 功能提取和数据清理提前数据工作流的一部分。|
|在文件中输出预测| 输出预测到表，以避免数据移动。 换行预测应用程序中直接访问的存储过程的函数。|

## <a name="best-practices"></a>最佳做法

+ 提前记下依赖项，例如所需的包。 在开发和测试环境中，也许可以将包安装为代码的一部分，但在生产环境中，这是一种不好的做法。 通知管理员，以便在部署代码之前可以安装和测试包。

+ 针对可能的数据类型问题创建一份查检表。 记录应在代码的每个部分中的结果的架构。

+ 确定主要数据源（例如模型训练数据或用于预测的输入数据），以及辅助源（例如因子、附加分组变量，等等）。 将最大的数据集映射到 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 的输入参数。

+ 更改输入数据语句，以便直接在数据库中操作。 而不是将数据移到本地的 CSV 文件，或进行重复 ODBC 调用，你可以更好的性能通过使用 SQL 查询，也可以直接对数据库，运行的视图避免数据移动。

+ 使用 SQL Server 查询计划来识别可以并行执行的任务。 如果输入的查询可以并行化，设置`@parallel=1`到你 arguments 的一部分[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 只要 SQL Server 可以处理分区表或者在多个进程之间分布查询并最终聚合结果，就通常可以使用此标志进行并行处理。

  如果用于训练模型的算法需要读取所有数据，或者你需要创建聚合，则通常无法使用此标志进行并行处理。

+ 如有可能，请将传统的 R 函数替换为支持分布式执行的 **ScaleR** 函数。 有关详细信息，请参阅[比较的基础 R 和缩放 R 函数](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler-compared-to-base-r)。

+ 检查 R 代码，确定是否可以独立执行某些步骤，或者可以使用单独的存储过程调用来更有效地执行某些步骤。 例如，你可能会决定单独执行特征工程或特征提取，并在新列中添加值。 

  使用 T-SQL 的而不是基于集的计算的 R 代码。 有关将 Udf 和 R 功能工程任务进行比较的 R 解决方案的示例，请参阅[数据科学端到端演练](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)。

+ 使用 R 包**sqlrutils**将你的代码转换为单个函数具有明确定义的输入和输出，可以轻松地映射到存储的过程参数。 有关详细信息和示例，请参阅[SqlRUtils](../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)。


## <a name="restrictions"></a>限制

 转换 R 代码时，请记住以下限制：

### <a name="data-types"></a>数据类型

-   支持所有 R 数据类型。 但是，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持的数据类型比 R 更广泛，因此，在将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据发送到 R 时，将执行某些隐式数据类型转换，反之亦然。 你可能还需要显式强制转换或将某些数据转换。

- 支持 NULL 值。 R 使用`na`数据构造来表示缺失值，这类似于 null。

有关详细信息，请参阅[R 库和数据类型](../r/r-libraries-and-data-types.md)。

### <a name="inputs-and-outputs"></a>“脚本转换编辑器”

+ 只能将一个输入数据集定义为存储过程参数的一部分。 存储过程的此输入查询可以是任一有效的单个 SELECT 语句。 我们建议你使用的最大的数据集，此输入并获取较小数据集根据需要使用 RODBC 对的调用。

+ 通过执行前面的存储的过程调用不能用作输入到[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

+ 输入数据集中的所有列必须映射到 R 脚本中的变量。 变量自动按名称映射。 例如，假定你的 R 脚本包含一个公式如下所示：
    
    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
     如果输入数据集不包含具有匹配名称 ArrDelay、 CRSDepTime、 DayOfWeek、 CRSDepHour 和 DayOfWeek 的列，则会引发错误。

+ 也可以提供多个标量参数作为输入。 但是，作为 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 存储过程的参数传入的任何变量必须映射到 R 代码中的变量。 默认情况下，变量按名称映射。

+ 若要在 R 代码的输出中包含标量输入变量，只需在定义变量时追加 **OUTPUT** 关键字。

+ 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中，R 代码限制为输出单个数据集作为 data.frame 对象。 但是，你也可以输出多个标量输出，包括采用 binary 格式的绘图，以及采用 varbinary 格式的模型。

+ 通常，可以使用 WITH RESULT SETS UNDEFINED 输出 R 脚本返回的数据集，而无需指定输出列的名称。 但是，要输出的 R 脚本中的任何变量必须映射到 SQL 输出参数。

+ 如果 R 脚本使用参数 `@parallel=1`，则必须定义输出架构。 原因是 SQL Server 可能会创建多个进程来并行运行查询，最后收集结果。 因此，可以创建并行进程之前，必须定义输出架构。

### <a name="dependencies"></a>依赖关系

 + 避免从 R 代码安装包。 在 SQL Server 上应提前安装包。
 
  请务必将包安装到机器学习服务使用的默认包库。 有关详细信息，请参阅[for SQL Server 的 R 包管理](../r/r-package-management-for-sql-server-r-services.md)

