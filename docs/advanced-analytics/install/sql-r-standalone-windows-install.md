---
title: "安装 SQL Server 2016 R Server （独立） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 48f28b7a8d357e80e7defb6d6a8d446041380fbf
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/21/2018
---
# <a name="install-sql-server-2016-r-server-standalone"></a>安装 SQL Server 2016 R Server （独立）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何使用 SQL Server 2016 安装程序安装的独立版本**SQL Server 2016 R 服务器**。 如果你有企业版或软件保障，在生产服务器上安装独立 R Server 是免费的。

## <a name="bkmk_prereqs"> </a> 预安装清单

SQL Server 2016 是必需的。 如果你有 SQL Server 自 2017 年，请安装[SQL Server 自 2017 年 1 机器学习服务器 （独立）](sql-machine-learning-standalone-windows-install.md)相反。

如果你安装 Revolution Analytics 工具或包的任何以前的版本，你必须先卸载它们。 

## <a name="get-the-installation-media"></a>获取安装介质

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

 ###  <a name="bkmk_ga_instalpatch"></a> 安装修补程序要求 

Microsoft 已发现特定版本的 Microsoft VC++ 2013 运行时二进制文件存在问题，这些二进制文件是作为 SQL Server 系统必备进行安装的。 如果未安装适用于该 VC 运行时二进制文件的更新，则在某些情况下 SQL Server 可能会遇到稳定性问题。 在安装 SQL Server 之前，请按照 [SQL Server 发行说明](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)中的说明来确定你的电脑是否需要 VC 运行时二进制文件的修补程序。  

## <a name="run-setup"></a>运行安装程序

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。

1. 启动 SQL Server 2016 安装向导。 我们建议你安装 Service Pack 1 或更高版本。

2. 上**安装**选项卡上，单击**新 R Server （独立） 安装**。
    
     ![启动的 R Server 独立安装程序](media/2016-setup-installation-rsvr.png "启动的 R Server 独立安装程序")
    
3.  在“功能选择”  页上，应已选择以下选项：
    
    **R Server（独立版）**  
    
    ![功能选择 R Server 独立](media/2016setup-rserver-features.png "功能 R Server 独立的选择")
    
    应忽略所有其他选项。 
    
    > [!NOTE]
    > 请避免先安装**共享功能**如果你运行安装程序的计算机上其中 R Services 已安装的 SQL Server 数据库中分析。 这将创建重复的库。
    > 
    > 由 SQL Server，以免与其他数据库引擎服务使用的内存发生冲突，在 SQL Server 中运行的 R 脚本进行管理，而独立 R Server 没有此类约束，并可能会干扰其他数据库操作。
    > 
    > 我们通常建议你安装 R Server （独立版） 的单独计算机上从 SQL Server R Services （数据库）。

4.  接受下载和安装 Microsoft R Open 的许可条款。 当“接受”  按钮变为不可用时，可以单击“下一步” 。
    
    这些组件，以及它们可能需要的任何系统必备组件的安装过程可能需要一段时间。
    
5.  在“准备安装”  页上，验证选择，并单击“安装” 。

## <a name="default-installation-folders"></a>默认安装文件夹

安装 R Server 使用 SQL Server 安装程序，R 库安装在与用于安装的 SQL Server 版本关联的文件夹中。 在此文件夹中，你会发现示例数据、 R 基程序包，文档和文档的 R 工具和运行时。

但是，如果你安装 Microsoft R Server 使用单独的 Windows installer （不 SQL 安装程序），或者升级使用单独的 Windows installer，R 库安装在不同的文件夹。

虽然我们不建议，如果同一台计算机上也安装的 SQL Server R Services （数据库） 的实例，但 R 库和工具的第二个副本被安装的其他文件夹中。

下表列出每个安装的路径。

|版本| 安装方法 | 默认文件夹|
|----|----|----|
|R Server (Standalone) |SQL Server 2016 安装程序向导|`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|R Server (Standalone) |Windows 独立安装程序|`C:\Program Files\Microsoft\R Server\R_SERVER`|
|机器学习服务器（独立） |  自 2017 年 SQL Server 安装向导中，与 R 语言选项 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER`|
|机器学习服务器（独立） |  自 2017 年 SQL Server 安装向导中，与 Python 语言选项 |`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|机器学习服务器（独立） |  Windows 独立安装程序 |`C:\Program Files\Microsoft\R Server\R_SERVER`|
|R Services（数据库内） |SQL Server 2016 安装程序向导|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|
|机器学习服务（数据库内） |自 2017 年 SQL Server 安装向导中，与 R 语言选项|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  |
|机器学习服务（数据库内） |自 2017 年 SQL Server 安装向导中，与 Python 语言选项| `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |

## <a name="development-tools"></a>开发工具

开发 IDE 不会安装安装程序的一部分。 不需要其他工具，如所有标准工具，将包括，将向你提供的 R 或 Python 的分布。

我们建议你尝试的新发行版[!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]或[for Visual Studio 的 Python](https://docs.microsoft.com/en-us/visualstudio/python/installing-python-support-in-visual-studio)。 Visual Studio 支持同时 R 和 Python，以及数据库开发工具，与 SQL Server 的连接和 BI 工具。 但是，你可以使用任何首选的开发环境，包括 RStudio。
  
## <a name="get-help"></a>获取帮助

需要安装或升级的帮助？ 常见的问题和已知的问题的答案，请参阅以下文章：

* [升级和安装常见问题-机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要检查实例的安装状态并修复常见的问题，请尝试这些自定义报表。

* [SQL Server R Services 的自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何使用 SQL Server 的基础知识。 下一步，请参阅以下链接：

+ [教程： 在 T-SQL 中运行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)。
+ [针对 R 开发人员的教程： 在数据库中分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

若要查看的机器学习基于实际方案的示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。

