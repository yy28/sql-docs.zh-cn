---
title: 升级 SQL Server R 实例 （机器学习服务） 中的 R 和 Python 组件 |Microsoft 文档
description: 升级 R 和 SQL Server 2016 R Services 或 SQL Server 自 2017 年 1 机器学习 Services sqlbindr.exe 用于绑定到机器学习服务器中的 Python。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 716fbd8a105164d40bfa6b3e67d126067174dc5a
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="upgrade-machine-learning-r-and-python-components-in-sql-server-instances"></a>升级 SQL Server 实例中的机器学习 （R 和 Python） 组件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 中的 R 和 Python 集成包括开放源代码和 Microsoft 专有包。 在标准 SQL Server 维护，R 和 Python 包更新根据 SQL Server 发布周期，具有到在当前版本的现有包的 bug 修补程序。 

大多数数据科研人员都习惯于使用较新的包变得可用。 对于 SQL Server 自 2017 年 1 机器学习 Services （数据库） 和 SQL Server 2016 R Services （数据库），你可以通过更改获取较新版本的 R 和 Python*绑定*从 SQL Server 维护到[Microsoft机器学习服务器](https://docs.microsoft.com/en-us/machine-learning-server/index)和[现代生命周期支持策略](https://support.microsoft.com/help/30881/modern-lifecycle-policy)。

绑定不会更改你的安装的基础知识： R 和 Python 集成仍是数据库引擎实例的一部分授权不变的 （无额外成本与绑定关联），并且 SQL Server 支持策略仍保留的数据库引擎。 但重新绑定如何维护 R 和 Python 包会更改。 本文的其余部分介绍的绑定机制及其工作原理的每个版本的 SQL Server。

> [!NOTE]
> 绑定适用于仅 （数据库） 实例。 绑定是不相关 （独立） 安装。

**SQL Server 2017**

对于 SQL Server 自 2017 年 1 机器学习服务，你应仅在 Microsoft 机器学习 Server 开始提供其他包或已有通过你的较新版本时，才考虑绑定。

**SQL Server 2016**

对于 SQL Server 2016 R Services 客户，有两个路径可用来获取新的和更新的 R 程序包。 一种需要升级到 SQL Server 2017;其次，绑定到 Microsoft 机器学习服务器。

升级到 SQL Server 2017 获取你的 R 程序包处包含在该版本中，以及 Python 功能的版本。 或者，绑定获取你更新的 R 包，可以进一步在 Microsoft 机器学习 Server 的每个新的主版本号和次版本刷新。 

绑定未提供 Python 支持，这是 SQL Server 2017 功能。 

**可通过 Microsoft 机器学习服务器组件升级**

下表是一个版本代码图，显示与 SQL Server，可能的升级绑定到 Microsoft 机器学习 Server （以前称为 R Server Python 支持从 MLS 9.2.1 加法之前） 时一同安装的版本。 

请注意绑定并不保证 R 或 Anaconda 的最新版本。 当绑定到 Microsoft 机器学习服务器时，可以通过安装程序，可能也可能不是在 web 上找到可用的最新版本安装的 R 或 Python 版本。

[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

组件 |初始版本 | R Server 9.0.1 | R Server 9.1 | MLS 9.2.1 | MLS 9.3 |
----------|----------------|----------------|--------------|---------|-------|
通过 R 的 Microsoft R Open (MRO) | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/achine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[预先训练的模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.a. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.a. | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.a. | 1.0 |  1.0 |  1.0 |  1.0 |


[**SQL Server 自 2017 年 1 机器学习服务**](../install/sql-machine-learning-services-windows-install.md)

组件 |初始版本 | MLS 9.3 | | | |
----------|----------------|---------|-|-|-|-|
通过 R 的 Microsoft R Open (MRO) | R 3.3.3 | R 3.4.3 | | | |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 | | | |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 | | | |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 | | | |
Anaconda 4.2 通过 Python 3.5  | 4.2/3.5.2 | 4.2/3.5.2 | | | |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3| | | |
 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3| | | |
[预先训练的模型](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3| | | |

## <a name="how-component-upgrade-works"></a>组件升级的工作原理

组件升级是通过*绑定*到的 SQL Server 2016 R Services 实例 （或 SQL Server 自 2017 年 1 机器学习 Services 实例） [Microsoft 机器学习 Server](https://docs.microsoft.com/machine-learning-server/index)。 

Microsoft 机器学习服务器是本地服务器产品分隔来自 SQL Server，但具有相同的解释程序和包。 绑定交换出 SQL Server 服务更新机制，以便你可以使用的 R 包和 Python 包传送与 Microsoft 机器学习服务器，这通常是日期早于 SQL Server 安装的。 切换支持策略是需要更高版本生成 R 数据科学团队吸引力和其解决方案的 Python 模块。 

通过执行绑定[MLS installer](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)。 安装更新特定的 R 和 Python 包，但不是将替换的独立且断开连接的服务器安装的 SQL Server 数据库中实例。

+ 不绑定，R 和 Python 包时你安装 SQL Server service pack 或累积更新 (CU) 对于 bug 修复修补。 
+ 使用绑定，则较新的包版本可以应用于您的实例，不考虑 CU 版本计划下[现代生命周期策略](https://support.microsoft.com/help/30881/modern-lifecycle-policy)和版本的 Microsoft 机器学习 Server。 现代的生命周期支持策略更短、 一年使用期限相比具有更频繁的更新。 绑定后，你将继续在变得 Microsoft 机器学习 Server 中提供的 R 和 Python 的将来更新中使用 MLS 安装程序。

绑定适用于 R 和 Python 功能。 也就是说，R 和 Python 功能 （Microsoft R Open、 Anaconda） 和专有的开放源代码包包 RevoScaleR、 revoscalepy，等。 绑定不会更改的数据库引擎实例的支持模型并不会更改 SQL Server 的版本。

绑定是可逆的。 你可以还原到 SQL Server 维护由[取消绑定实例](#bkmk_Unbind)和修复 SQL Server 数据库引擎实例。

计算总和，绑定的步骤如下所示：

+ 使用现有的配置安装的 SQL Server 2016 R Services （或 SQL Server 自 2017 年 1 机器学习服务） 启动。
+ 确定哪个版本的 Microsoft 机器学习服务器具有你想要使用的升级的组件。
+ 下载并运行该版本的安装程序。 安装程序检测到的现有实例，添加一个绑定的选项，并返回兼容的实例的列表。
+ 选择你想要将绑定并完成安装程序以执行绑定的实例。

在用户体验方面技术，并且您与它的工作方式保持不变。 唯一的区别是存在较新版本的包和可能的其他包最初可通过 SQL Server （如 SQL Server 2016 R Services 客户 MicrosoftML)。

## <a name="bkmk_BindWizard"></a>将绑定到 MLS 使用安装程序

Microsoft 机器学习安装程序检测到的现有功能和 SQL Server 版本，并调用名为 SqlBindR.exe 若要更改绑定的实用工具。 在内部，SqlBindR 是链接到安装程序，间接使用。 更高版本，你可以直接从命令行以执行特定的选项调用 SqlBindR。

1. 验证你的服务器满足最低版本要求。 对于 SQL Server 2016 R 服务，最小值是[Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276)和[CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)。 在 SSMS 中，运行`SELECT @@version`返回服务器版本信息。 

1. 检查以确认现有的版本比你打算将其替换为更小的 R 和 RevoScaleR 的版本。 对于 SQL Server 2016 R 服务，R 基本包很 3.2.2 以及 RevoScaleR 8.0.3。

    + 请转到 files\microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\bin
    + 双击**R**打开控制台。
    + 若要获取程序包版本，请使用`library(help="base")`和`library(help="RevoScaleR")`。 

1. 下载到具有你想要升级的实例的计算机上的 Microsoft 机器学习服务器。 我们建议[最新版本](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)。

1. 解压缩文件夹并启动 ServerSetup.exe，位于 MLSWIN93。

   ![Microsoft 机器学习 Server 安装向导](media/mls-921-installer-start.PNG)

1. 上**配置安装**，确认要升级的组件，并查看兼容的实例的列表。 

   在左侧，选择你想要保留还是升级每个功能。 不能升级某些功能并不是其他。 空的复选框中删除该功能，而假定当前已安装。 在屏幕截图中，给定的 SQL Server 2016 R Services (MSSQL13) 实例选择 R 和预先训练的模型的 R 版本。 此配置是有效的因为 SQL Server 2016 支持 R，但不是 Python 支持。

   在右侧，选择实例名称旁边的复选框。 如果未不列出任何实例，则必须组合不兼容。 如果不选择实例，创建新的独立安装机器学习 Server 后，和 SQL Server 库保持不变。 如果您不能选择一个实例，则可能不是在[SP1 CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1)。 

    ![Microsoft 机器学习 Server 安装向导](media/mls-931-installer-mssql13.png)

1. 上**许可协议**页上，选择**我接受这些条款**机器学习服务器接受许可条款。 

1. 在后续页上，提供以选择，如 Microsoft R Open 或 Python Anaconda 分发任何开放源代码组件的其他许可条件的同意。

1. 上**几乎存在**页上，记下的安装文件夹。 默认文件夹是 \Program Files\Microsoft\ML 服务器。

    如果你想要更改安装文件夹，请单击**高级**以返回到向导的第一页。 但是，你必须重复所有以前的选择。

在安装过程中，替换为 SQL Server 使用的任何 R 或 Python 库和快速启动板更新为使用较新的组件。 因此，如果实例以前使用的默认 R_SERVICES 文件夹中的库，升级后这些库已删除并快速启动板服务的属性将更改以在新位置中使用的库。

绑定会影响这些文件夹的内容： C:\Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\library 替换 C:\Program Files\Microsoft\ML Server\R_SERVER 的内容。 由 Microsoft 机器学习 Server 安装程序创建第二个文件夹及其内容。 

如果升级失败，请检查[SqlBindR 错误代码](#sqlbindr-error-codes)有关详细信息。

## <a name="confirm-binding"></a>确认绑定

重新检查以确认你拥有较新版本的 R 和 RevoScaleR 的版本。 使用与你的数据库引擎实例中的 R 包一起分发的 R 控制台来获取包信息：

+ 请转到 files\microsoft SQL Server\MSSQL13。MSSQLSERVER\R_SERVICES\bin
+ 双击**R**打开控制台。
+ 若要获取程序包版本，请使用`library(help="base")`和`library(help="RevoScaleR")`。 

对于绑定到机器学习服务器 9.3 SQL Server 2016 R Services，R 基程序包应为 3.4.1、 RevoScaleR 应 9.3，并还应该 MicrosoftML 9.3。 

如果你添加预先训练的模型，模型都嵌入到 MicrosoftML 库和你可通过 MicrosoftML 函数对其进行调用。 有关详细信息，请参阅[MicrosoftML 的 R 示例](https://docs.microsoft.com/machine-learning-server/r/sample-microsoftml)。

## <a name="offline-no-internet-access"></a>脱机 （没有 internet 访问）

对于未连接 internet 的系统，可以安装程序和.cab 文件，下载到连接 internet 的计算机，然后将文件传输到独立的服务器。 

安装程序 (ServerSetup.exe) 包括 Microsoft 包 （RevoScaleR、 MicrosoftML、 olapR、 sqlRUtils）。 .Cab 文件提供了其他核心组件。 例如，"SRO"cab 提供 R Open，Microsoft 的分发的开放源代码。

下面的说明解释如何放置的脱机安装文件。

1. 下载 MLS 安装程序。 它将作为单个 zip 文件下载。 我们建议[最新版本](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer)，但你也可以安装[早期版本](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)。

1. 下载.cab 文件。 以下链接是 9.3 版本。 如果你需要早期版本，可以在中找到更多链接[R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components)。 回想一下，Python/Anaconda 可以仅添加到 SQL Server 自 2017 年 1 机器学习 Services 实例。 R 和 Python; 已存在预先训练的模型.cab 提供了正在使用的语言中的模型。

    | 功能 | 下载 |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | 预先训练的模型 | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. 将.zip 和.cab 文件传输到目标服务器。

1. 在服务器上，键入`%temp%`中运行命令，以获取临时目录的物理位置。 物理路径因计算机，但通常是`C:\Users\<your-user-name>\AppData\Local\Temp`。

1. 在 %temp%文件夹中的 Place.cab 文件。

1. 解压缩安装。

1. 运行 ServerSetup.exe，并按照屏幕上的提示完成安装。

## <a name="bkmk_BindCmd"></a>命令行操作

在运行 Microsoft 机器学习服务器后，名为 SqlBindR.exe 的命令行实用工具将变为可用，你可将用于进一步绑定操作。 例如，如果您决定要反转一个绑定，您无法重新运行安装程序或使用命令行实用工具。 此外，此工具可用于为实例检查兼容性和可用性。

> [!TIP]
> 找不到 SqlBindR？ 你可能不具有运行安装程序。 仅在运行机器学习 Server 安装程序之后，SqlBindR 才可用。

1. 以管理员身份打开命令提示符并导航到包含 sqlbindr.exe 的文件夹。 默认位置是 C:\Program Files\Microsoft\MLServer\Setup

2. 键入以下命令，查看可用实例列表： `SqlBindR.exe /list`
  
   记下所列出的完整实例名称。 例如，实例名称可能是 MSSQL14。默认实例，或 SERVERNAME 类似 MSSQLSERVER。MYNAMEDINSTANCE。

3. 运行**SqlBindR.exe**命令 */绑定*自变量，并指定要升级，实例的名称使用上一步中返回的实例名称。

   例如，若要升级的默认实例，请键入：  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. 完成升级后，重新启动任何实例已修改与关联的快速启动板服务。

## <a name="bkmk_Unbind"></a>还原或取消绑定实例

你可以还原到初始安装的 R 和 Python 的组件，建立 SQL Server 安装程序的绑定的实例。 有三个部分恢复为 SQL Server 服务。

+ [步骤 1： 取消绑定从 Microsoft 机器学习服务器](#step-1-unbind)
+ [步骤 2： 将实例还原为原始状态](#step-2-restore)
+ [步骤 3： 重新安装任何添加到安装的程序包](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>步骤 1： 取消绑定

有两个对回滚绑定选项： 重新重新运行安装程序或使用 SqlBindR 命令行实用程序。

#### <a name="bkmk_wizunbind"></a> 取消绑定使用安装程序

1. 找到的安装程序机器学习服务器。 如果你已删除安装程序，你可能需要再次下载或将其复制从另一台计算机。
2. 请确保具有你想要取消绑定的实例的计算机上运行安装程序。
2. 安装程序会标识适用于取消绑定的候选项的本地实例。
3. 取消选择你想要还原到原始配置实例旁边的复选框。
4. 接受许可协议。 在安装时，必须指示你接受许可条款偶数。
5. 单击 **“完成”**。 该进程花费一段时间。

#### <a name="bkmk_cmdunbind"></a> 取消绑定使用命令行

1. 如上节所述，打开命令提示符并导航到包含 **sqlbindr.exe** 的文件夹。

2. 在使用 */unbind* 参数的情况下运行 **SqlBindR.exe** 命令，并指定实例。

   例如，以下命令将恢复默认实例：
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>步骤 2： 修复的 SQL Server 实例

运行 SQL Server 安装程序修复具有 R 和 Python 功能的数据库引擎实例。 将保留现有的更新，但如果你错过了任何 SQL Server 服务对 R 和 Python 包的更新，此步骤将应用这些修补程序。

或者，这是更多工作，但无法完全卸载和重新安装数据库引擎实例，并将所有的服务更新。

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>步骤 3： 添加任何第三方包

可能具有到包库添加了其他开放源代码或第三方包。 由于反转绑定切换默认包库的位置，你必须重新安装程序包添加到 R，但现在使用 Python 库。 有关详细信息，请参阅[默认包](installing-and-managing-r-packages.md)，[安装新的 R 包](install-additional-r-packages-on-sql-server.md)，和[安装新的 Python 软件包](../python/install-additional-python-packages-on-sql-server.md)。

## <a name="known-issues"></a>已知问题

本部分列出了已知的问题特定于使用 SqlBindR.exe 实用工具中，或可能会影响 SQL Server 实例的计算机学习服务器的升级。

### <a name="restoring-packages-that-were-previously-installed"></a>还原以前安装的程序包

如果你升级到 Microsoft R Server 9.0.1，该版本的版本的 SqlBindR.exe 无法还原原始包或 R 组件完全，要求用户在实例中，运行 SQL Server 修复应用所有的服务版本，然后重新启动实例。

更高版本的 SqlBindR 自动还原原始的 R 功能，无需重新安装的 R 组件，或重新修补程序服务器。 但是，你必须安装可能在初始安装后添加任何 R 程序包更新。

如果已使用包管理角色来安装并共享包，此任务是要容易得多： 你可以使用 R 命令同步到文件系统在数据库中，使用记录的已安装的程序包，反之亦然。 有关详细信息，请参阅[for SQL Server 的 R 包管理](r-package-management-for-sql-server-r-services.md)。

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>从 SQL Server 的多个升级的问题

如果运行的新安装 Microsoft R Server 9.1.0 程序时，你有以前升级到 9.0.1，SQL Server 2016 R Services 的实例，它将显示所有的有效实例的列表，然后默认情况下，选择以前绑定的实例。 如果继续，则以前绑定的实例是未绑定。 因此，更早版本 9.0.1 删除安装，包括任何相关的包，但未安装 Microsoft R Server (9.1.0) 的新版本。

一种解决方法，您可以修改现有的 R Server 安装，如下所示：
1. 在 Control Panel 中，打开**添加或删除程序**。
2. 找到 Microsoft R Server，并单击**更改/修改**。
3. 安装程序启动时，选择你想要将绑定到 9.1.0 的实例。

Microsoft 机器学习 Server 9.2.1 和 9.3 不具有此问题。

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>绑定或取消绑定离开多个临时文件夹

有时也无法清理临时文件夹的绑定和正在取消绑定操作。
如果您发现具有类似名称的文件夹，则可以删除它在安装完成后： R_SERVICES_<guid>

> [!NOTE]
> 请务必等待，直到安装已完成。 它可能需要很长时间才能删除关联使用某一版本的 R 库，然后添加新的 R 库。 操作完成后，会删除临时文件夹。

## <a name="sqlbindrexe-command-syntax"></a>SqlBindR.exe 命令语法

### <a name="usage"></a>用法

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parameters

|名称|Description|
|------|------|
|*list*| 显示当前计算机上所有 SQL 数据库实例 ID 的列表|
|*bind*| 将指定的 SQL 数据库实例升级至 R Server 最新版本，并确保实例会自动获取 R Server 的未来升级|
|*unbind*|从指定的 SQL 数据库实例中卸载 R Server 最新版本，并防止未来 R Server 升级影响该实例|

< a name ="sqlbinder 错误代码"<a/>

### <a name="errors"></a>错误

该工具返回以下错误消息：

|错误代码  | 消息           | 详细信息               |
|------------|-------------------|-----------------------|
|将绑定错误 | 确定 （成功） | 无错误通过绑定。 |
|将绑定错误 1 | 参数无效 | 语法错误。 |
|将绑定错误 2 | 无效的操作 | 语法错误。 |
|将绑定错误 3 | 无效的实例 | 实例存在，但不是有效的绑定。 |
|将绑定错误 4 | 不绑定 | |
|将绑定错误 5 | 已绑定 | 已运行 *bind* 命令，但指定的实例已绑定。 |
|将绑定错误 6 | 绑定失败 | 取消绑定实例时出错。 |
|将绑定错误 7 | 未绑定 | 数据库引擎实例已 R Services 或 SQL Server 计算机学习 Services。 实例未绑定到 Microsoft 机器学习 Server。 |
|将绑定错误 8 | 取消绑定失败 | 取消绑定实例时出错。 |
|将绑定错误 9 | 未找到任何实例 | 在此计算机上未不找到任何实例。 |


## <a name="see-also"></a>另请参阅

+ [安装机器学习用于 Windows 的服务器 (Internet 连接)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [安装机器学习用于 Windows 的服务器 （脱机）](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [机器学习 Server 中的已知的问题](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [从以前的版本中的 R Server 的功能公告](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [已弃用，不再使用或更改的特性](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)