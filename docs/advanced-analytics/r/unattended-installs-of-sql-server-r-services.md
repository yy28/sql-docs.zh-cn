---
title: "无人参与的安装的机器学习服务 |Microsoft 文档"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 18
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: babb74aa866404853cfef83e1d30159354f385e7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="unattended-installation-of-machine-learning-services-in-database"></a>机器学习服务 （数据库） 的无人参与的安装

本主题介绍如何使用命令行自变量与 SQL Server 安装程序来安装数据库引擎，在静默模式下的实例中的机器学习。 在无人参与安装中，你不使用安装向导中，交互式功能，必须提供到完整安装，包括许可协议，SQL Server 及机学习组件所需的所有自变量。

**适用于：** SQL Server 2016 R Services、 SQL Server 自 2017 年 1 机器学习服务 （数据库）

> [!IMPORTANT]
> 
> 在 SQL Server 2016 和 SQL Server 自 2017 年中，附加步骤是必需的这是之后安装程序完成后，启用的功能。 其中包括重新配置和重新启动的实例。 请务必查看所有步骤。

## <a name="prerequisites"></a>先决条件

+ 你必须在你将在其中使用机器学习每个实例上安装数据库引擎。

+ 如果计算机没有 Internet 访问权限，请务必安装机器事先学习组件的安装程序。 有关下载位置，请参阅[安装没有 Internet 访问权限的机器学习组件](../../advanced-analytics/r/installing-ml-components-without-internet-access.md)。

+ 有新许可的组件相关的开放源代码 R 和 Python 的参数。 你必须接受许可条款使用单独的自变量为你安装的每种语言。 如果未在命令行中包括此参数，安装将失败。

+ 若要完成安装程序，而无需响应提示，请确保你已标识包括授权，以及任何其他功能，你可能想要安装的所有必需的参数。

> [!NOTE] 
> 在早期版本中需要支持 SQL 登录名的混合的安全模式。 但是，你可能考虑启用混合模式身份验证，以支持通过使用 SQL 登录名的数据科学家解决方案开发。

## <a name="bkmk_NewInstall"></a>使用 R 的机器学习服务的无人参与的安装

下面的示例演示**最小**要执行无提示，无人参与时在命令行中指定的所需的功能安装的 SQL Server 自 2017 年机 Services （数据库）。

1. 打开提升的命令提示符，并运行以下命令：

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
    ```
    
    请注意所需的 SQL Server 自 2017 年中的 R 的标志： `ADVANCEDANALYTICS`， `SQL_INST_MR`，和`IACCEPTROPENLICENSETERMS`。
2. 重新启动服务器。
3. 执行安装后配置步骤中所述[本节](#bkmk_PostInstall)。 另一个需要重新启动计算机的 SQL Server 服务。

## <a name="OldInstall"></a>无人参与的安装的 R Services （数据库）
 
 下面的示例演示**最小**所需的功能来执行无提示，无人参与时在命令行中指定的 SQL Server 2016 R Services 安装。

1. 打开提升的命令提示符，并运行以下命令：

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
    ```
    请注意 2016 R SERVICES 所需的标志：`ADVANCEDANALYTICS`和`IACCEPTROPENLICENSETERMS`。
2. 重新启动服务器。
3. 执行安装后配置步骤中所述[本节](#bkmk_PostInstall)。 另一个需要重新启动计算机的 SQL Server 服务。

## <a name = "bkmk_PostInstall"></a>安装完成后的其他步骤

1.  安装完成后，打开一个新**查询**中的窗口[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，并运行以下命令以启用功能。
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  你必须显式启用该功能并重新配置;否则，它将不能调用外部脚本，即使已安装的功能。
  
2.  重新启动 SQL Server 实例的服务的重新配置。 这样将自动重新启动相关[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]以及服务。

3. 如果有自定义安全配置，或者如果要使用 SQL Server 支持远程计算上下文，则可能需要执行其他步骤。 有关详细信息，请参阅[升级和安装常见问题](../../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md)。

