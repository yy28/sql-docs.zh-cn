---
title: 安装 R 语言和没有 internet 访问权限的 SQL Server 机器学习的 Python 组件
description: 脱机或已断开连接机器学习 R 和 Python 安装程序在网络防火墙后面的独立 SQL Server 实例上。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/13/2019
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 37cd555ec099b11c6dbf792ff5f4e0ac869a0792
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2019
ms.locfileid: "57976317"
---
# <a name="install-sql-server-machine-learning-r-and-python-on-computers-with-no-internet-access"></a>安装 SQL Server 机器学习在没有 internet 访问权限的计算机上的 R 和 Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

默认情况下，安装程序连接到 Microsoft 下载站点以获取所需的和更新的组件，用于实现SQL Server 上的机器学习功能。 如果防火墙的限制会阻止安装程序访问这些站点，可以使用连接到 internet的设备下载文件，将文件传输到脱机的服务器，然后运行安装程序。

数据库内分析包括数据库引擎实例，以及用于R和Python集成的其他组件，具体取决于SQL Server的版本。 

+ SQL Server 2017 包括 R 和 Python 
+ SQL Server 2016 的仅限 R 的。

在独立服务器上，通过CAB文件添加机器学习和特定于R/Python语言的功能。 

## <a name="sql-server-2017-offline-install"></a>SQL Server 2017 脱机安装

要在独立服务器上安装SQL Server 2017机器学习服务（R和Python），首先要下载SQL Server的初始版本以及用于提供R和Python支持的相应CAB文件。 即使计划立即更新服务器以使用最新的累积更新，仍然需要先安装初始版本。

> [!Note]
> SQL Server 2017没有Service Pack。 这是SQL Server第一个将初始版本作为唯一基准的版本，且仅通过累积更新来进行维护。 

### <a name="1---download-2017-cabs"></a>1-下载 2017 cab 文件

在连接到Internet的计算机上，下载CAB文件，为初始版本和SQL Server 2017的安装媒体提供R和Python功能。 

发行版本  |下载链接  |
---------|---------------|
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python Open     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python Server    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |

###  <a name="2---get-sql-server-2017-installation-media"></a>2-获取 SQL Server 2017 安装介质

1. 在具有 internet 连接的计算机上, 下载[SQL Server 2017 安装程序](https://www.microsoft.com/sql-server/sql-server-downloads)。 

2. 双击安装程序并选择**下载媒体**安装类型。 使用此选项，安装程序将创建包含安装介质的本地.iso （或.cab） 文件。

   ![选择安装类型的下载媒体](media/offline-download-tile.png "下载媒体")

## <a name="sql-server-2016-offline-install"></a>SQL Server 2016 脱机安装

SQL Server 2016数据库内分析仅限R，仅包含两个CAB文件，分别用于产品包和Microsoft开源R分发。 首先安装这些版本之一：RTM, SP 1, SP 2. 基础安装到位后，便可应用累积更新。

在连接到Internet的计算机上，下载安装程序使用的CAB文件，用于在SQL Server 2016上安装数据库内分析。 

### <a name="1---download-2016-cabs"></a>1-下载 2016 cab 文件

发行版本  | Microsoft R Open | Microsoft R Server |
---------|-----------------|---------------------|
**SQL Server 2016 RTM**     | [SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266) |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051) |
**SQL Server 2016 SP 1**     | [SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879) |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881) | 
**SQL Server 2016 SP 2**  |[SRO_3.2.2.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866039) |[SRS_8.0.3.20000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866038) |

### <a name="2---get-sql-server-2016-installation-media"></a>2-获取 SQL Server 2016 安装媒体

首次安装时，可以在目标计算机上安装SQL Server 2016 RTM、SP 1或SP 2。 这些版本都可以接受累积更新。

获取包含安装媒体的.iso文件的一种方式是通过[Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/)来实现。 登录，然后使用**下载**链接查找要安装的SQL Server 2016版本。 下载内容是一个.iso文件，可以将其复制到目标计算机进行脱机安装。

## <a name="transfer-files"></a>传输文件

将 SQL Server 安装介质 （.iso 或.cab） 和数据库内分析 CAB 文件复制到目标计算机。 在目标计算机，例如安装程序用户的 %temp * 文件夹上的相同文件夹中放置的 CAB 文件和安装媒体文件。

在 %TEMP%文件夹是必需的 Python CAB 文件。 对于 R，可以使用 %TEMP%或将 myrcachedirectory 参数设置为 CAB 路径。

下面的屏幕截图显示了 SQL Server 2017 CAB 和 ISO 文件。 SQL Server 2016 下载看起来不同： 较少的文件 (没有 Python) 和安装媒体文件的名称是 2016。

![要传输的文件列表](media/offline-file-list.png "文件列表")

## <a name="run-setup"></a>运行安装程序

从 internet 断开连接的计算机上运行 SQL Server 安装程序时，安装程序将添加**脱机安装**到向导页，以便您可以指定你在上一步中复制的 CAB 文件的位置。

1. 若要开始安装，请双击要访问的安装介质的.iso 或.cab 文件。 应会看到**setup.exe**文件。

2. 右键单击**setup.exe**并以管理员身份运行。

3. 当安装向导显示的开源 R 或 Python 组件的许可页时，单击**接受**。 接受许可条款，可继续执行下一步。

4. 当您到达**脱机安装**页上，在**安装路径**，指定包含前面复制的 CAB 文件的文件夹。

   ![Cab 文件夹选择的向导页](media/screenshot-sql-offline-cab-page.png "CAB 文件夹")

5. 继续以下屏幕上的提示完成安装。

<a name="apply-cu"></a>

## <a name="apply-cumulative-updates"></a>应用累积更新

我们建议将最新的累积更新应用到数据库引擎和机器学习组件。 通过安装程序安装累积更新。 

1. 使用基线实例启动。 您仅适用于 SQL Server 的现有安装累积更新：

  + SQL Server 2017 初始版本
  + SQL Server 2016 初始版本、 SQL Server 2016 SP 1 或 SQL Server 2016 SP 2

2. 在 internet 上连接了设备，请转到你的 SQL Server 版本的累积更新列表：

  + [SQL Server 2017 更新](https://sqlserverupdates.com/sql-server-2017-updates/)
  + [SQL Server 2016 更新](https://sqlserverupdates.com/sql-server-2016-updates/)

3. 选择最新累积更新来下载该可执行文件。

4. 对 R 和 Python 中获取相应的 CAB 文件。 有关下载链接，请参阅[实例上 SQL Server 数据库内分析的累积更新的下载 CAB](sql-ml-cab-downloads.md)。

5. 传输所有文件、 可执行文件和 CAB 文件，在脱机计算机上的同一文件夹。

6. 运行安装程序。 接受许可条款，然后在功能选择页面上，查看应用累积更新的功能。 应会看到每一项功能为当前实例，包括机器学习功能安装。

  ![从功能树选择功能](media/cumulative-update-feature-selection.png "功能列表")

5. 继续完成向导，接受 R 和 Python 分发版的许可条款。 在安装期间，系统会提示选择包含已更新的 CAB 文件的文件夹位置。

## <a name="set-environment-variables"></a>设置环境变量

对于仅 R 功能集成，应设置**MKL_CBWR**环境变量[确保一致的输出](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr)从 Intel Math Kernel Library (MKL) 的计算。

1. 在控制面板中，单击**系统和安全** > **系统** > **高级系统设置** >  **环境变量**。

2. 创建一个新的用户或系统变量。 

  + 到组变量名称 `MKL_CBWR`
  + 将变量的值设置为 `AUTO`

此步骤需要重新启动服务器。 如果你是要启用脚本执行，您可以在重启保持，直到完成所有配置工作。

## <a name="post-install-configuration"></a>安装后配置

安装完成后，重新启动服务，然后配置服务器以启用脚本执行：

+ [启用外部脚本执行 (SQL Server 2017)](sql-machine-learning-services-windows-install.md#bkmk_enableFeature)
+ [启用外部脚本执行 (SQL Server 2016)](sql-r-services-windows-install.md#bkmk_enableFeature)

SQL Server 2017 机器学习服务或 SQL Server 2016 R Services 的初始脱机安装需要联机安装相同的配置：

+ [验证安装是否](sql-machine-learning-services-windows-install.md#verify-installation)(对于 SQL Server 2016 中，单击[此处](sql-r-services-windows-install.md#verify-installation))。
+ [根据需要其他配置](sql-machine-learning-services-windows-install.md#additional-configuration)(对于 SQL Server 2016 中，单击[此处](sql-r-services-windows-install.md#bkmk_FollowUp))。

## <a name="next-steps"></a>后续步骤

若要检查的实例的安装状态并解决常见的问题，请参阅[自定义报表的 SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)。

与任何不熟悉的消息或日志条目的帮助，请参阅[升级和安装常见问题解答-机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)。

