---
title: 安装 SQL Server 自 2017 年 1 机器学习 Server （独立） |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1c56d3cb9420d8d0e48ec936008d0351d5d32eb4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="install-sql-server-2017-machine-learning-server-standalone-on-windows"></a>安装 SQL Server 自 2017 年 1 机器学习 Windows 上的服务器 （独立）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 安装程序包括用于安装的机器学习在 SQL Server 外部运行的服务器的选项。 此选项可能会很有用，如果你需要开发高性能计算机学习解决方案，可以使用远程计算上下文、 本地服务器与远程计算机学习服务器之间的 Spark 群集上或在另一个 SQL Server 上互换切换实例。
  
本文介绍如何使用 SQL Server 安装程序安装的独立版本**SQL Server 自 2017 年 1 机器学习服务器**。 

## <a name="bkmk_prereqs"> </a> 预安装清单

SQL Server 2017 是必需的。 如果你有 SQL Server 2016，请安装[SQL Server 2016 R Server （独立）](sql-r-standalone-windows-install.md)相反。

如果安装了以前的版本，如 SQL Server 2016 R Server （独立） 或 Microsoft R Server 卸载现有的安装才能继续。

## <a name="get-the-installation-media"></a>获取安装介质

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>运行安装程序

对于本地安装，必须以管理员身份运行安装程序。 如果从远程共享安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须使用对远程共享具有读取和执行权限的域帐户。

1. 启动 SQL Server 2017 年 1 安装向导。

2. 单击**安装**选项卡，然后选择**新计算机学习 Server （独立） 安装**。
    
     ![安装机器学习服务器独立](media/2017setup-installation-page-mlsvr.png "启动机器学习 Server 独立安装")

3. 规则检查完成后，请接受 SQL Server 许可条款，然后选择新的安装。

4. 上**功能选择**页上，以下选项应已处于选中状态：

    - Microsoft 机器学习 Server （独立）

    - 默认值同时选中 R 和 Python。 您可以取消选中其中任一种语言，但我们建议你安装至少一个受支持的语言。

     ![安装机器学习服务器独立](media/2017setup-features-page-mlsvr-rpy.png "启动机器学习 Server 独立安装")
    
    应忽略所有其他选项。 
    
    > [!NOTE]
    > 请避免先安装**共享功能**如果计算机已安装的 SQL Server 数据库中分析的机器学习服务。 这将创建重复的库。
    > 
    > 此外，在 SQL Server 中运行的 R 或 Python 脚本由 SQL Server，以免与其他数据库引擎服务使用的内存发生冲突，而独立机器学习服务器没有此类约束，并且可能会干扰其他数据库操作. 最后，数据库管理员通常阻止通过 RDP 会话中，它通常用于操作化，远程访问。
    > 
    > 出于这些原因，我们通常建议你从 SQL Server 机器学习服务的单独计算机上安装机器学习 Server （独立）。

5.  接受许可条款下载和安装机器学习组件。 如果你安装这两种语言，单独的许可协议则需要为 Microsoft R 和 Python。
    
     ![Python 许可协议](media/2017setup-python-license.png "Python 许可协议")
    
    这些组件，以及它们可能需要的任何系统必备组件的安装过程可能需要一段时间。 当“接受”  按钮变为不可用时，可以单击“下一步” 。

6.  在“准备安装”  页上，验证选择，并单击“安装” 。

### <a name="default-installation-folders"></a>默认安装文件夹

安装 R Server 时或使用 SQL Server 安装程序的机器学习服务器，R 库安装在与用于安装的 SQL Server 版本关联的文件夹。 在此文件夹中，你会发现示例数据、 R 基程序包，文档和文档的 R 工具和运行时。

但是，如果使用单独的 Windows 安装程序中，安装或升级使用单独的 Windows installer，R 库安装在不同的文件夹。

只是为了引用，如果你已安装的 SQL Server 实例与 R Services （数据库） 或机器学习服务 （数据库中），并且该实例是在同一台计算机，R 库和工具默认安装在其他文件夹中。

下表列出每个安装的路径。

|版本| 安装方法 | 默认文件夹|
|----|----|----|
|SQL Server 自 2017 年 1 机器学习服务器 （独立） |  自 2017 年 SQL Server 安装向导 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft 机器学习 Server （独立） |  Windows 独立安装程序 |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server 自 2017 年 1 机器学习服务 （数据库） |自 2017 年 SQL Server 安装向导中，与 R 语言选项|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server （独立） |  SQL Server 2016 安装程序向导 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services （数据库） |SQL Server 2016 安装程序向导|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

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

+ [教程： 在 T-SQL 中运行 R](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [针对 R 开发人员的教程： 在数据库中分析](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 开发人员可以了解如何将 Python 用于 SQL Server 按照这些教程：

+ [教程： 在 T-SQL 中运行 Python](../tutorials/run-python-using-t-sql.md)
+ [面向 Python 开发人员的教程： 在数据库中分析](../tutorials/sqldev-in-database-python-for-sql-developers.md)

若要查看的机器学习基于实际方案的示例，请参阅[机器学习教程](../tutorials/machine-learning-services-tutorials.md)。
