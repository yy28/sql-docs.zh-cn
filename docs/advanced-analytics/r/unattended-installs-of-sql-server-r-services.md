---
title: "无人参与的安装的机器学习服务 |Microsoft 文档"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: f1c7aaf35c0c58e9a7aab3c5b31725f586ffd2ac
ms.sourcegitcommit: 6bd21109abedf64445bdb3478eea5aaa7553fa46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2018
---
# <a name="unattended-installation-of-machine-learning-services-in-database"></a>机器学习服务 （数据库） 的无人参与的安装
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何使用命令行自变量包含 SQL Server 安装程序来安装机器学习组件。

无人参与安装，是指你不使用安装向导中的交互式功能和改为提供所需完成安装，包括许可协议，SQL Server 及机学习组件上的所有自变量命令行或脚本，通常在静默模式下的一部分。

+ [SQL Server 2016 R Services](#bkmk_OldInstall)
+ [SQL Server 自 2017 年 1 机器学习服务](#bkmk_NewInstall)与 R 或 Python
+ [Microsoft R Server 或机器学习服务器](../r/install-microsoft-r-server-from-the-command-line.md)

**适用于： SQL Server 自 2017 年 1 机器学习服务 （数据库中），SQL Server 2016 R Services**

## <a name="prerequisites"></a>必要條件

+ 你必须在你将在其中使用机器学习每个实例上安装数据库引擎。

+ 如果计算机没有 Internet 访问权限，请务必下载机器事先学习组件的安装程序。 请参阅[安装没有 Internet 访问权限的机器学习组件](../r/installing-ml-components-without-internet-access.md)。

+ 有单独的 R 和 Python 开放源代码组件的每个授权参数。 SQL Server 2016 支持仅 R;SQL Server 2017 支持 R 和 Python。 你必须接受你安装的每种语言的许可条款。 如果你未在命令行中包括此参数，则安装将失败。

+ 若要完成安装程序，而无需响应提示，请确保你已标识包括授权，以及任何其他功能，你可能想要安装的所有必需的参数。

+ **混合**支持 SQL 登录名的安全模式需要在早期版本中。 尽管不再是必需的但你可能考虑启用混合模式身份验证，以支持通过使用 SQL 登录名的用户数据科学家解决方案开发。

> [!IMPORTANT]
> 
> 在完成安装程序以启用该功能后，则需要其他步骤。 其中包括重新配置和重新启动的实例。 请务必查看上一节中的所有项[安装后步骤](#bkmk_PostInstall)以确定需要在安装完成后的操作。

## <a name="bkmk_NewInstall"></a>  有关 SQL Server 自 2017 年的命令行安装

下面的示例包括**最小**的功能要求。

> [!IMPORTANT]
> 请确保从提升的命令提示符运行所有命令。
> 
> 安装完成后，执行一些其他步骤是必需的。 请参阅[本节](#bkmk_PostInstall)。 
> 配置完成后，将需要的 SQL Server 服务的另一个重新启动。

### <a name="install-r-only"></a>仅安装 R

下面的示例演示使用添加 R 语言安装的 SQL Server 自 2017 年机 Services （数据库） 的所需执行无提示，无人参与的参数。

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
```

请注意所需的 SQL Server 自 2017 年中的 R 的标志：

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MR`
+ `IACCEPTROPENLICENSETERMS`中创建已分区表或索引。

### <a name="install-python-only"></a>仅安装 Python

下面的示例演示使用添加 Python 语言安装的 SQL Server 自 2017 年机 Services （数据库） 的所需执行无提示，无人参与的参数。

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

请注意所需的 SQL Server 自 2017 年中的 Python 的标志：

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MPY`
+ `IACCEPTPYTHONOPENLICENSETERMS`

### <a name="install-both-r-and-python-on-a-named-instance"></a>命名实例上安装 R 和 Python

下面的示例演示执行无提示，无人参与所需的自变量安装的 SQL Server 自 2017 年机 Services （数据库） 的命名实例上。 添加 R 和 Python 的语言。

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER.ServerName /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

## <a name="OldInstall"></a> SQL Server 2016 命令行安装
 
下面的示例演示使用添加 R 语言安装的 SQL Server 2016 的所需执行无提示，无人参与的参数。

```
Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
```

请注意 2016 R Services 所需的标志：

+ `ADVANCEDANALYTICS`
+ `IACCEPTROPENLICENSETERMS`

## <a name = "bkmk_PostInstall"></a>安装完成后的其他步骤

在 SQL Server 安装程序完成后，无论你安装哪个版本后，你必须执行以下步骤。 机器学习功能未启用默认情况下，并且必须显式启用。

1.  安装完成后，打开一个新**查询**中的窗口[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，并运行以下命令以启用功能。
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  你必须显式启用该功能并重新配置;否则，它将不能调用外部脚本，即使已安装的功能。
  
2.  重新启动 SQL Server 实例的服务的重新配置。 这样将自动重新启动相关[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]以及服务。

> [!IMPORTANT]
> 
> 如果你有一个自定义安全配置，或者如果你将使用 SQL Server 作为计算上下文从远程客户端执行 R 或 Python 代码时，可能需要一些附加步骤。 
> 
> 有关详细信息，请参阅[升级和安装常见问题解答](../../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md)。
