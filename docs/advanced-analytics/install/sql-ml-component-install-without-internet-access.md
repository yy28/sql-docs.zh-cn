---
title: 安装 SQL Server 机器学习组件没有 internet 访问权限 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/02/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 289f304cf445882981fb110e9c00a395cac90e5f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34585609"
---
# <a name="install-sql-server-machine-learning-components-without-internet-access"></a>安装 SQL Server 机器学习没有 internet 访问权限的组件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

默认情况下，安装程序连接到 Microsoft 下载站点，以获取必需和更新的组件的机器学习在 SQL Server 上。 如果防火墙约束阻止访问这些站点安装，你可以使用 internet 连接的设备下载文件，将文件传输到脱机的服务器，然后运行安装程序。

## <a name="get-the-installation-media"></a>获取安装介质

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

> [!NOTE]  
> 对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。  
 
 ###  <a name="bkmk_ga_instalpatch"></a> 安装修补程序要求 

Microsoft 已发现特定版本的 Microsoft VC++ 2013 运行时二进制文件存在问题，这些二进制文件是作为 SQL Server 系统必备进行安装的。 如果未安装适用于该 VC 运行时二进制文件的更新，则在某些情况下 SQL Server 可能会遇到稳定性问题。 在安装 SQL Server 之前，请按照 [SQL Server 发行说明](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)中的说明来确定你的电脑是否需要 VC 运行时二进制文件的修补程序。  


## <a name="download-cab-files"></a>下载.cab 文件

在连接 internet 的服务器上，下载脱机安装所需的.cab 文件。 安装程序使用.cab 文件来安装补充的功能。

发行版本  |下载链接  |
---------|---------|
**SQL Server 2017 初始版本** |
Microsoft R Open     |[SRO_3.3.3.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851496)|
Microsoft R Server      |[SRS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851507)|
Microsoft Python 打开     |[SPO_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851502) |
Microsoft Python 服务器    |[SPS_9.2.0.24_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851508) |
**SQL Server 2017 CU1** |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server      |[SRS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851501)|
Microsoft Python 打开     |无更改;使用以前 |
Microsoft Python 服务器    |[SPS_9.2.0.100_1033.cab](https://go.microsoft.com/fwlink/?LinkId=851500) |
**SQL Server 自 2017 年 CU2** |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server      |无更改;使用以前|
Microsoft Python 打开     |无更改;使用以前|
Microsoft Python 服务器    |无更改;使用以前|
**SQL Server 自 2017 年 1 CU3** |
Microsoft R Open     |[SRO_3.3.3.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863894)|
Microsoft R Server      |[SRS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863893)|
Microsoft Python 打开     |无更改;使用以前|
Microsoft Python 服务器    |[SPS_9.2.0.300_1033.cab](https://go.microsoft.com/fwlink/?LinkId=863892)|
**SQL Server 自 2017 年 CU4** |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server      |[SRS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866212&clcid=1033)|
Microsoft Python 打开     |无更改;使用以前|
Microsoft Python 服务器    |[SPS_9.2.0.400_1033.cab](https://go.microsoft.com/fwlink/?LinkId=866213&clcid=1033)|
**SQL Server 自 2017 年 CU5** |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server      |[SRS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869052&clcid=1033)|
Microsoft Python 打开     |无更改;使用以前|
Microsoft Python 服务器    |[SPS_9.2.0.500_1033.cab](https://go.microsoft.com/fwlink/?LinkId=869053&clcid=1033)|
**SQL Server 自 2017 年 CU6** |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server      |[SRS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871074&clcid=1033)|
Microsoft Python 打开     |无更改;使用以前|
Microsoft Python 服务器    |[SPS_9.2.0.600_1033.cab](https://go.microsoft.com/fwlink/?LinkId=871073&clcid=1033)|
**SQL Server 自 2017 年 CU7** |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server      |o 更改，则为使用以前|
Microsoft Python 打开     |无更改;使用以前|
Microsoft Python 服务器    |无更改;使用以前|


### <a name="bkmk_2016Installers"></a>SQL Server 2016 的的下载

> [!IMPORTANT]
> 
> 在安装 SQL Server 2016 SP1 CU4 或 SP1 CU5 脱机时，下载 SRO_3.2.2.16000_1033.cab。 如果在安装程序对话框中所示，可以从 FWLINK 831785 下载 SRO_3.2.2.13000_1033.cab，重命名文件作为 SRO_3.2.2.16000_1033.cab 安装累积更新之前。

发行版本  |下载链接  |
---------|---------|
**SQL Server 2016 RTM**     |
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)
**SQL Server 2016 CU 1**     |
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)
**SQL Server 2016 CU 2**     |
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)
**SQL Server 2016 CU 3**     |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server     | 无更改;使用以前 |
**SQL Server 2016 CU 4**     |
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831785)|
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)|
**SQL Server 2016 CU 5**     |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server     |无更改;使用以前|
**SQL Server 2016 CU 6**     |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server     |[SRS_8.0.3.14000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850316)  |
**SQL Server 2016 CU 7**     |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server     |无更改;使用以前 |
**SQL Server 2016 SP 1**     |
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)
**SQL Server 2016 SP 1 CU1**     |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server     |无更改;使用以前|
**SQL Server 2016 SP 1 CU2**     |
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)|
Microsoft R Server    |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)|
**SQL Server 2016 SP 1 CU3**     |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server     |无更改;使用以前|
**SQL Server 2016 SP 1 CU4 和 GDR**     |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server    |[SRS_8.0.3.17000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=850317)
**SQL Server 2016 SP 1 CU5**     |
Microsoft R Open     |无更改;使用以前|
Microsoft R Server    |无更改;使用以前 |

如果你想要查看 Microsoft R 的源代码，它是可供下载的存档文件采用.tar 格式：[下载 R Server 安装程序](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows#download)

### <a name = "bkmk_OtherComponents"></a>附加的先决条件

根据所用的环境，可能需要为以下必备组件创建安装程序的本地副本。

组件  |版本
---------|---------
[Microsoft AS OLE DB Provider for SQL Server 2016](https://go.microsoft.com/fwlink/?linkid=834405)     |  13.0.1601.5
[Microsoft .NET Core](https://go.microsoft.com/fwlink/?linkid=834319)     | 1.0.1
[Microsoft MPI](https://go.microsoft.com/fwlink/?linkid=834316)     | 7.1.12437.25
[Microsoft Visual C++ 2013 Redistributable](https://go.microsoft.com/fwlink/?linkid=799853)     | 12.0.30501.0
[Microsoft Visual C++ 2015 Redistributable](https://go.microsoft.com/fwlink/?linkid=828641)     | 14.0.23026.0

## <a name="transfer-files"></a>传输文件

传输压缩的 SQL Server 安装介质和已下载到在其安装安装程序的计算机的文件。

如放在方便的文件夹的 CAB 文件**下载**或安装程序用户的临时文件夹： < 用户名 > C:\Users \AppData\Local\Temp。

将 en_sql_server_2017.iso 文件放在方便的文件夹。 双击**setup.exe**以开始安装。

### <a name="run-setup"></a>运行安装程序

从 internet 断开连接的计算机上运行 SQL Server 安装程序时，安装程序会添加**脱机安装**到向导页，以便你可以指定你在上一步中复制的.cab 文件的位置。

1. 启动 SQL Server 安装向导。

2. 当安装向导显示开放源代码 R 或 Python 组件的授权页时，单击**接受**。 接受许可条款，可继续执行下一步。

3. 在**脱机安装**页上，在**安装路径**，指定包含你前面记的.cab 文件的文件夹。

4. 继续以下屏幕上的提示完成安装。

安装完成后，请重新启动服务，然后配置服务器以中所述启用脚本执行[安装 SQL Server 自 2017 年 1 机器学习 Services （数据库）](sql-machine-learning-services-windows-install.md)或[安装 SQL Server2016 R Services （数据库）](sql-r-services-windows-install.md)。

## <a name="slipstream-upgrades-for-offline-servers"></a>脱机的服务器的版本补充升级

补充安装是指对失败的实例安装应用修补或更新，以修复现有的问题。 此方法的优点在于，可以在执行安装的同时更新 SQL Server，避免以后单独重新启动。

+ 如果服务器无法访问 Internet，则在开始执行更新过程**之前**，必须下载 SQL Server 安装程序，然后下载 R 组件安装程序的匹配版本。  默认情况下，与 SQL Server 不包括 R 组件。

+ 如果要向现有安装添加这些组件，使用 SQL Server 安装的更新的版本和其他组件的相应更新的版本。 指定要安装的 R 功能时，安装程序将查找匹配的版本为机器学习组件的安装程序。

## <a name="get-help"></a>获取帮助

需要安装或升级的帮助？ 常见的问题和已知的问题的答案，请参阅以下文章：

* [升级和安装常见问题-机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要检查实例的安装状态并修复常见的问题，请尝试这些自定义报表。

* [SQL Server R Services 的自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

由 R 服务支持团队这篇文章演示如何在 SQL Server 2016 中执行的无人参与的安装或升级 R services:[在没有 Internet 访问权限的计算机上部署 R Services](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)。


## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何使用 SQL Server 的基础知识。 下一步，请参阅以下链接：

+ [教程： 在 T-SQL 中运行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [针对 R 开发人员的教程： 在数据库中分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 开发人员可以了解如何将 Python 用于 SQL Server 按照这些教程：

+ [教程： 在 T-SQL 中运行 Python](../tutorials/run-python-using-t-sql.md)
+ [面向 Python 开发人员的教程： 在数据库中分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

若要查看的机器学习基于实际方案的示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。

