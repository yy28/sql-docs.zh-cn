---
title: 安装 SQL Server 2016 R Server （独立版） |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e5457698120536247ad1823b842bb1b8e52b484d
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979279"
---
# <a name="install-sql-server-2016-r-server-standalone"></a>安装 SQL Server 2016 R Server （独立版）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何使用 SQL Server 2016 安装程序安装的独立版本**SQL Server 2016 R Server**。

## <a name="bkmk_prereqs"> </a> 预安装清单

SQL Server 2016 是必需的。 如果您有 SQL Server 2017，请安装[SQL Server 2017 机器学习服务器 （独立版）](sql-machine-learning-standalone-windows-install.md)相反。

如果安装任何以前版本的 Revolution Analytics 工具或包，必须先卸载它们。 

## <a name="get-the-installation-media"></a>获取安装介质

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

 ###  <a name="bkmk_ga_instalpatch"></a> 安装修补程序要求 

Microsoft 已发现特定版本的 Microsoft VC++ 2013 运行时二进制文件存在问题，这些二进制文件是作为 SQL Server 系统必备进行安装的。 如果未安装适用于该 VC 运行时二进制文件的更新，则在某些情况下 SQL Server 可能会遇到稳定性问题。 在安装 SQL Server 之前，请按照 [SQL Server 发行说明](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch)中的说明来确定你的电脑是否需要 VC 运行时二进制文件的修补程序。  

## <a name="run-setup"></a>运行安装程序

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。

1. 启动 SQL Server 2016 安装向导。 我们建议你安装 Service Pack 1 或更高版本。

2. 上**安装**选项卡上，单击**新的 R Server （独立版） 安装**。
    
     ![启动的 R Server 独立版的安装程序](media/2016-setup-installation-rsvr.png "启动的 R Server 独立版的安装程序")
    
3.  在“功能选择”  页上，应已选择以下选项：
    
    **R Server（独立版）**  
    
    ![功能选择 R Server 独立版](media/2016setup-rserver-features.png "功能选择 R Server 独立版")
    
    应忽略所有其他选项。 
    
    > [!NOTE]
    > 避免安装**共享功能**如果您运行安装程序的计算机上的 R Services 已安装的 SQL Server 数据库内分析。 这会创建重复的库。
    > 
    > SQL Server 中运行 R 脚本由 SQL Server，以免与其他数据库引擎服务使用的内存发生冲突，而独立 R Server 没有此类约束，并可能会干扰其他数据库操作。
    > 
    > 我们通常建议安装 R Server （独立版） 的单独计算机上从 SQL Server R Services （数据库内）。

4.  接受下载和安装 Microsoft R Open 的许可条款。 当“接受”  按钮变为不可用时，可以单击“下一步” 。
    
    这些组件和它们可能需要的任何系统必备组件的安装可能需要一些时间。
    
5.  在“准备安装”  页上，验证选择，并单击“安装” 。

## <a name="default-installation-folders"></a>默认安装文件夹

在安装 R Server 使用 SQL Server 安装程序时，R 库安装在用于安装的 SQL Server 版本关联的文件夹。 在此文件夹中，您将找到示例数据、 R 基础包文档和文档的 R 工具和运行时。

但是，如果您安装 Microsoft R Server 使用单独的 Windows 安装程序 （不 SQL 安装程序），或使用单独的 Windows 安装程序升级，R 库安装在其他文件夹。

不过，我们建议反对这样做，如果同一台计算机上还安装了 R Services （数据库内） 的 SQL Server 的实例，R 库和工具的第二个副本安装在不同的文件夹。

下表列出了每个安装的路径。

|版本| 安装方法 | 默认文件夹|
|----|----|----|
|R Server (Standalone) |SQL Server 2016 安装向导|`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|R Server (Standalone) |Windows 独立安装程序|`C:\Program Files\Microsoft\R Server\R_SERVER`|
|机器学习服务器（独立） |  SQL Server 2017 安装程序向导中，使用 R 语言选项 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER`|
|机器学习服务器（独立） |  SQL Server 2017 安装程序向导中，使用 Python 语言选项 |`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|机器学习服务器（独立） |  Windows 独立安装程序 |`C:\Program Files\Microsoft\R Server\R_SERVER`|
|R Services（数据库内） |SQL Server 2016 安装向导|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|
|机器学习服务（数据库内） |SQL Server 2017 安装程序向导中，使用 R 语言选项|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  |
|机器学习服务（数据库内） |SQL Server 2017 安装程序向导中，使用 Python 语言选项| `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |

## <a name="development-tools"></a>开发工具

开发 IDE 未安装的一部分安装。 不需要其他工具，如，提供了所有标准工具，将提供使用分布的 R 或 Python。

我们建议尝试的新版本[!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)]或[Visual Studio 的 Python](https://docs.microsoft.com/visualstudio/python/installing-python-support-in-visual-studio)。 Visual Studio 支持同时 R 和 Python，以及数据库开发工具，与 SQL Server 的连接和 BI 工具。 但是，可以使用任何喜欢的开发环境，包括 RStudio。
  
## <a name="get-help"></a>获取帮助

需要安装或升级的帮助？ 常见的问题和已知的问题的答案，请参阅以下文章：

* [升级和安装常见问题解答-机器学习服务](../r/upgrade-and-installation-faq-sql-server-r-services.md)

若要检查的实例的安装状态并解决常见的问题，请尝试这些自定义报表。

* [SQL Server R Services 的自定义报表](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>后续步骤

R 开发人员可以开始使用一些简单的示例，并了解 R 如何与 SQL Server 配合工作的基础知识。 下一步，请参阅以下链接：

+ [教程： 在 T-SQL 中运行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)。
+ [教程： 在数据库内分析 R 开发人员](../tutorials/sqldev-in-database-r-for-sql-developers.md)

若要查看的机器学习基于实际方案的示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。

