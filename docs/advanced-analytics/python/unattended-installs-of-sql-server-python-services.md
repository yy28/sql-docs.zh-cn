---
title: "无人参与的安装的 Python 机器学习服务 （数据库） |Microsoft 文档"
ms.custom: 
ms.date: 07/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: r-services
ms.component: python
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a159a3198037e21664bb9b07647a01b1d5317d22
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="unattended-installation-of-python-machine-learning-services-in-database"></a>无人参与的安装的 Python 机器学习服务 （数据库）

本主题介绍如何在 SQL Server 2017 安装程序中使用命令行自变量使用机器学习服务和 Python，使用静默模式安装的 SQL Server 数据库引擎。

> [!NOTE]
> 不要忘记包含许可协议，一个用于 Python，一个用于 SQL Server 的命令行参数。

## <a name="prerequisites"></a>必备条件

在开始安装过程之前，请注意以下要求：

+ 无法独立于 SQL Server 2017 数据库引擎安装 Python 服务。 必须包括 SQL 数据库引擎功能。
+ 如果您正在执行脱机安装，必须提前下载所需的 Python 组件并将它们复制到本地文件夹。 有关下载位置，请参阅[安装机器学习 Components without Internet Access](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md)。
+ 没有新的参数， */IACCEPTPYTHONLICENSETERMS*，指示已接受使用 Continuum 分析提供的 Python 组件的许可条款。 如果未在命令行中包括此参数，安装将失败。
+ 若要完成安装程序，而无需响应提示，请确保你已标识包括适用于 Python 和 SQL Server 的许可，以及任何其他功能，你可能想要安装的所有必需的参数。
+  在某些预发行版本的 SQL Server 2016 需要混合的模式身份验证。 它不再必需的但它可能会在其中数据科学家进行开发和测试远程使用 SQL 登录名的解决方案的情况下很有用。

## <a name="perform-an-unattended-installation-of-python-machine-learning-services-in-database"></a>执行 Python 机器学习服务 （数据库） 的无人参与的的安装

下面的示例演示**最小**时的默认实例上执行 Python 和数据库引擎的无提示、 无人参与安装命令行中指定的功能要求。

> [!NOTE]
> 此功能需要 SQL Server 自 2017 年。 在早期版本的 SQL Server 不支持 Python。

1. 打开提升的命令提示符，并运行以下命令：

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONLICENSETERMS
    ```

    > [!NOTE]
    > 
    > 有新的安装程序标志 for Python:`SQL_INST_MPY`和`IACCEPTPYTHONLICENSETERMS`

2. 指引，请重新启动服务器。
3. 执行安装后配置步骤中所述[本节](#bkmk_PostInstall)。 另一个需要重新启动计算机的 SQL Server 服务。

## <a name = "bkmk_PostInstall"></a>安装后步骤

1.  安装完成后，打开一个新**查询**中的窗口[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，并运行以下命令以启用功能。

    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  你必须显式启用该功能并重新配置;否则，它将不能调用外部脚本，即使已安装的功能。
  
3.  重新启动 SQL Server 实例的服务的重新配置。 这样将自动重新启动相关[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]以及服务。

3. 如果有自定义安全配置，或者如果要使用 SQL Server 支持远程计算上下文，则可能需要执行其他步骤。 有关详细信息，请参阅[机器学习安装程序疑难解答](../machine-learning-troubleshooting-faq.md)。
