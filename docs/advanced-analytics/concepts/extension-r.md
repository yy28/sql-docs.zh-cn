---
title: SQL Server 中的 R 扩展 |Microsoft Docs
description: 了解有关 R 代码执行和 SQL Server 中的内置 R 库。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: af71b03238a744702288f1f7411a5ebec3911f60
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43892853"
---
# <a name="r-extension-in-sql-server"></a>SQL Server 中的 R 扩展
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

R 扩展是到关系数据库引擎的 SQL Server 机器学习服务外接程序的一部分。 它将添加 R 执行环境、 使用标准库和工具，基础 R 发行版和 Microsoft R 库： [RevoScaleR](../r/revoscaler-overview.md)进行按规模、 分析[MicrosoftML](../using-the-microsoftml-package.md)为机器学习算法和其他用于访问数据或 SQL Server 中的 R 代码库。

R 集成是从 SQL Server 2016 中的 SQL Server 中提供[R Services](../r/sql-server-r-services.md)，并继续向前作为的一部分[SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)。

## <a name="r-components"></a>R 组件

SQL Server 包含的开源和专有的包。 基本的 R 库安装通过 Microsoft 的分发的开放源代码: Microsoft R 打开 (MRO)。 R 的当前用户应该能够移植其 R 代码并将其作为 SQL Server 上具有少或没有修改的外部进程中执行。 MRO 安装独立于 SQL 工具和可扩展性框架中的核心引擎进程之外执行。 在安装期间，您必须同意的开源许可条款。 此后，可以运行标准 R 包，无需进一步修改，就像在任何其他开放源代码分发的。 

SQL Server 不会修改基本的 R 可执行文件，但必须使用的 R 安装安装程序，因为在该版本是专有的包生成，并可在测试版本。 MRO 不同之处可能会收到从 CRAN 的 R 基础分发的详细信息，请参阅[与 R 语言和 Microsoft R 产品和功能的互操作性](https://docs.microsoft.com/r-server/what-is-r-server-interoperability)。

可以与实例关联的文件夹中找到 R 基础包发行版安装程序安装。 例如，如果 SQL Server 2016 默认实例上安装 R Services，R 库位于此文件夹中默认情况下： `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`。 同样，与默认实例关联的 R 工具将位于此文件夹默认情况下： `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`。

Microsoft 通过添加并行和分布式工作负荷的 R 包包括以下库。

| 库 | Description |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 支持数据源对象和数据探索、 操作、 转换和可视化效果。 它支持远程计算上下文，以及各种可缩放的机器学习模型的创建，如**rxLinMod**。 这些 API 已经过优化，可以分析由于过大而无法装入内存的数据集，以及执行分布在多个核心或处理器之间的计算。 RevoScaleR 包还支持 XDF 文件格式来加速移动和数据分析时使用的存储。 XDF 格式使用纵栏表存储且可移植，可用于加载并处理来自各种来源（包括文本、SPSS 或 ODBC 连接）的数据。 |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | 包含机器学习算法，经过优化的速度和准确性，以及行中使用文本和图像的转换。 有关详细信息，请参阅[将 MicrosoftML 包与 SQL Server 使用](https://docs.microsoft.com/sql/advanced-analytics/using-the-microsoftml-package)。 | 

## <a name="using-r-in-sql-server"></a>在 SQL Server 中使用 R

您可以编写脚本 R 使用基本函数，但若要从多处理中受益，必须导入**RevoScaleR**并**MicrosoftML**到 R 代码，然后调用其函数来创建模型模块并行执行。 
 
支持的数据源包含 ODBC 数据库、 SQL Server 和 XDF 文件格式来交换数据使用其他源，或使用 R 解决方案。 输入的数据必须是表格。 必须在数据帧的形式返回所有 R 结果。

支持的计算上下文包括本地或远程 SQL Server 计算上下文。 远程计算上下文是指在工作站上，例如一台计算机启动的执行代码但开关，则脚本执行过程转移到远程计算机。 切换计算上下文需要两个系统都相同的 RevoScaleR 库。

本地计算上下文中，正如您所料，包括执行 T-SQL 代码与数据库引擎实例中相同的服务器上的 R 代码，或嵌入在存储过程。 此外可以从本地 R IDE 中运行代码并让脚本在 SQL Server 计算机上执行，通过定义远程计算上下文。

## <a name="execution-architecture"></a>执行体系结构

下图展示了 SQL Server 组件的交互与 R 运行时在每个受支持的方案： 从 R 命令行，使用 SQL Server 计算上下文中运行脚本，数据库和远程执行。

### <a name="r-scripts-executed-from-sql-server-in-database"></a>从 SQL Server 数据库中执行 R 脚本

从"内部"，然后通过调用存储的过程执行 SQL Server 运行的 R 代码。 因此，可以发出存储过程调用的任何应用程序都可以启动 R 代码的执行。  此后，SQL Server 管理执行 R 代码在下图中进行了总结。

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. 对 R 运行时发出的请求由传递给存储过程 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 的参数 _@language='R'_ 指示。 SQL Server 将此请求发送到快速启动板服务。
2. Launchpad 服务启动相应的启动器（在本例中为 RLauncher）。
3. RLauncher 启动外部 R 进程。
4. BxlServer 与 R 运行时，若要管理的 SQL Server 数据的交换和存储工作结果协调。
5. SQL Satellite 管理有关相关的任务和进程与 SQL Server 的通信。
6. BxlServer 使用 SQL Satellite 状态以及到 SQL Server 的结果进行通信。
7. SQL Server 获取结果并关闭相关的任务和流程。

### <a name="r-scripts-executed-from-a-remote-client"></a>从远程客户端执行 R 脚本

从支持 Microsoft R 的远程数据科学客户端连接时，可以使用 RevoScaleR 函数在 SQL Server 的上下文中运行 R 函数。 此工作流与前面的工作流不同，下图对此做了汇总。

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. 对于 RevoScaleR 函数，R 运行时调用链接的函数，后者接着调用 BxlServer。
2. BxlServer 已随附在 Microsoft R 中，在独立于 R 运行时的进程中运行。
3. BxlServer 确定连接目标并使用 ODBC 发起连接，传递 R 数据源对象的连接字符串中提供的凭据。
4. BxlServer 打开到 SQL Server 实例的连接。
5. 对于 R 调用，快速启动板服务调用，该服务接着启动相应的启动器 RLauncher。 然后，R 代码的处理过程类似于从 T-SQL 运行 R 代码。
6. RLauncher 调用到 SQL Server 计算机上安装的 R 运行时实例。
7. 将结果返回到 BxlServer。
8. SQL Satellite 管理与 SQL Server 和相关的作业对象清理的通信。
9. SQL Server 会将结果传递回客户端。

## <a name="see-also"></a>另请参阅

+ [SQL Server 中的可扩展性框架](extensibility-framework.md)
+ [Python 和机器学习中 SQL Server 的扩展](extension-python.md)