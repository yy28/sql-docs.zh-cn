---
title: R 编程语言扩展
description: 在 SQL Server 2016 R Services 或 SQL Server 2017 机器学习服务中了解 R 代码执行和内置 R 库。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3bf8e77cec92cde0e5a8adf4d3e1e36f1689b917
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343410"
---
# <a name="r-language-extension-in-sql-server"></a>SQL Server 中的 R 语言扩展
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

R 扩展是关系数据库引擎的 SQL Server 机器学习服务外接程序的一部分。 它添加 R 执行环境、具有标准库和工具的基本 R 分发版, 以及 Microsoft R 库:用于大规模分析的[RevoScaleR](../r/ref-r-revoscaler.md) 、用于机器学习算法的[MicrosoftML](../r/ref-r-microsoftml.md) , 以及用于访问 SQL Server 中的数据或 R 代码的其他库。

从 SQL Server 2016、 [r Services](../r/sql-server-r-services.md)开始 SQL Server 开始, 并在[SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)中继续进行 r 集成。

## <a name="r-components"></a>R 组件

SQL Server 包括开源和专用包。 基本 R 库通过 Microsoft 的开源版版本进行安装:Microsoft R Open (MRO)。 R 的当前用户应该能够移植其 R 代码, 并将其作为 SQL Server 上的外部进程执行, 只需进行少量修改或无需修改。 MRO 独立于 SQL 工具进行安装, 并在可扩展性框架中的核心引擎进程外执行。 在安装过程中, 必须同意开源许可证的条款。 此后, 你可以运行标准 R 包而无需进行进一步的修改, 就像 R 的任何其他开放源代码分发中一样。 

SQL Server 不会修改基本 R 可执行文件, 但必须使用安装程序安装的 R 版本, 因为该版本是专用包的生成和测试版本。 若要详细了解 MRO 如何不同于可能从 CRAN 获取的 R 的基本分发, 请参阅[与 r 语言和 Microsoft R 产品和功能的互操作性](https://docs.microsoft.com/r-server/what-is-r-server-interoperability)。

可以在与实例关联的文件夹中找到安装程序安装的 R 基包分发。 例如, 如果在 SQL Server 2016 默认实例上安装 R Services, 则默认情况下 R 库位于此文件夹中: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`。 同样, 默认情况下, 与默认实例关联的 R 工具将位于此文件夹中: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`。

Microsoft 为并行和分布式工作负荷添加的 R 包包含以下库。

| 库 | 描述 |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 支持数据源对象和数据浏览、操作、转换和可视化。 它支持创建远程计算上下文, 以及各种可缩放的机器学习模型, 如**rxLinMod**。 这些 API 已经过优化，可以分析由于过大而无法装入内存的数据集，以及执行分布在多个核心或处理器之间的计算。 RevoScaleR 包还支持 XDF 文件格式, 以便更快地移动和存储用于分析的数据。 XDF 格式使用纵栏表存储且可移植，可用于加载并处理来自各种来源（包括文本、SPSS 或 ODBC 连接）的数据。 |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | 包含经过优化以实现速度和准确性的机器学习算法, 以及用于处理文本和图像的行内转换。 有关详细信息, 请参阅[MicrosoftML in SQL Server](../r/ref-r-microsoftml.md)。 | 

## <a name="using-r-in-sql-server"></a>在 SQL Server 中使用 R

您可以使用基本函数编写 R 脚本, 但要从多处理中获益, 您必须将**RevoScaleR**和**MicrosoftML**模块导入 R 代码中, 然后调用其函数以创建并行执行的模型。 
 
支持的数据源包括 ODBC 数据库、SQL Server 和 XDF 文件格式, 以便与其他源或通过 R 解决方案交换数据。 输入数据必须为表格格式。 所有 R 结果必须以数据帧的形式返回。

支持的计算上下文包括本地或远程 SQL Server 计算上下文。 远程计算上下文指的是在一台计算机 (如工作站) 上启动的代码执行, 但随后会将脚本执行切换到远程计算机。 切换计算上下文要求两个系统都具有相同的 RevoScaleR 库。

如您所料, 本地计算上下文包括: 在与数据库引擎实例相同的服务器上执行 R 代码, 并在 T-sql 中或在存储过程中嵌入代码。 还可以通过定义远程计算上下文, 从本地 R IDE 运行代码, 并在 SQL Server 计算机上执行脚本。

## <a name="execution-architecture"></a>执行体系结构

以下关系图说明了在每个受支持的方案中 SQL Server 组件与 R 运行时的交互: 通过使用 SQL Server 计算上下文从 R 命令行运行脚本和远程执行。

### <a name="r-scripts-executed-from-sql-server-in-database"></a>从 SQL Server 数据库中执行 R 脚本

从 "内部" SQL Server 运行的 R 代码通过调用存储过程来执行。 因此，可以发出存储过程调用的任何应用程序都可以启动 R 代码的执行。  之后 SQL Server 管理 R 代码的执行, 如以下关系图所示。

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. 对 R 运行时发出的请求由传递给存储过程 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 的参数 _@language='R'_ 指示。 SQL Server 将此请求发送到快速启动板服务。
2. Launchpad 服务启动相应的启动器（在本例中为 RLauncher）。
3. RLauncher 启动外部 R 进程。
4. BxlServer 与 R 运行时进行协调, 以管理与工作结果 SQL Server 和存储的数据交换。
5. SQL 附属项管理有关与 SQL Server 相关的任务和进程的通信。
6. BxlServer 使用 SQL 附属项将状态和结果传递到 SQL Server。
7. SQL Server 获取结果并关闭相关任务和进程。

### <a name="r-scripts-executed-from-a-remote-client"></a>从远程客户端执行 R 脚本

从支持 Microsoft R 的远程数据科学客户端进行连接时, 可以使用 RevoScaleR 函数在 SQL Server 的上下文中运行 R 函数。 此工作流与前面的工作流不同，下图对此做了汇总。

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. 对于 RevoScaleR 函数, R 运行时调用链接函数, 该函数反过来调用 BxlServer。
2. BxlServer 已随附在 Microsoft R 中，在独立于 R 运行时的进程中运行。
3. BxlServer 确定连接目标并使用 ODBC 发起连接，传递 R 数据源对象的连接字符串中提供的凭据。
4. BxlServer 将打开与 SQL Server 实例的连接。
5. 对于 R 调用, 将调用快速启动板服务, 这会启动相应的启动程序 RLauncher。 然后，R 代码的处理过程类似于从 T-SQL 运行 R 代码。
6. RLauncher 对安装在 SQL Server 计算机上的 R 运行时实例进行调用。
7. 将结果返回到 BxlServer。
8. SQL 附属项管理与相关作业对象 SQL Server 和清理的通信。
9. SQL Server 将结果传递回客户端。

## <a name="see-also"></a>请参阅

+ [SQL Server 中的扩展性框架](extensibility-framework.md)
+ [SQL Server 中的 Python 和机器学习扩展](extension-python.md)