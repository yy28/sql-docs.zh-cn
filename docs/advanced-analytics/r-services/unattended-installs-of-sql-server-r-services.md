---
title: "SQL Server R Services 的无人参与安装 | Microsoft Docs"
ms.custom: 
ms.date: 02/10/2017
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
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5eabee1be4fd315c2675ba34f5f12a96619e1cb7
ms.lasthandoff: 04/11/2017

---
# <a name="unattended-installs-of-sql-server-r-services"></a>SQL Server R Services 的无人参与安装
    
本主题介绍如何使用 SQL Server 命令行参数在安静模式下安装启用了 R Services 的 SQL Server：即，不使用安装向导的交互式功能的无人参与安装。 

## <a name="prerequisites"></a>先决条件

在开始安装过程之前，请注意以下要求：

+ 必须在要使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的 R Services（数据库中）的每个实例上安装数据库引擎。  
+ 如果要执行脱机安装，必须提前下载所需的 R 组件并将它们复制到本地文件夹。 有关下载位置，请参阅 [在没有 Internet 连接的情况下安装 R 组件](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)。   
+ 有一个新参数 */IACCEPTROPENLICENSETERMS*，它指示已接受使用开源 R 组件的许可证条款。 如果未在命令行中包括此参数，安装将失败。 
+ 若要完成安装而无需对提示做出响应，请确保已提供所有必需的参数，包括用于 R 和 SQL Server 许可的参数，以及用于你可能想要安装的任何其他功能的参数。 
  
## <a name="perform-an-unattended-install-of-r-services-in-database"></a>执行 R Services (In-Database) 的无人参与安装  
 下面的示例演示了在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中执行 R Services 的静默无人参与安装时，要在命令行中指定的**最低**必需功能。  
  
###  <a name="bkmk_Unattended"></a>  
  
1. 在提升的命令提示符下运行以下命令：  

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,AdvancedAnalytics /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS  
    ```  
    > [!NOTE] 
    > 仅在早期版本中需要使用 SQL 安全模式。 但是，混合模式身份验证通常已在开发人员要使用 SQL 登录名连接到 SQL Server 的数据科学方案中使用。

## <a name="post-installation-steps"></a>安装后步骤  

2.  完成安装之后，先在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中运行以下命令以启用该功能。  
  
    ```  
    EXEC sp_configure  'external scripts enabled', 1  
    RECONFIGURE WITH OVERRIDE   
    ```  
  
    > [!NOTE]  
    >  必须显式启用该功能并重新进行配置；否则，它将无法调用 R 脚本，即使已安装该功能也是如此。  
  
3.  重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 此操作也会自动重启相关的 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务。  

3. 如果有自定义安全配置，或者如果要使用 SQL Server 支持远程计算上下文，则可能需要执行其他步骤。 有关详细信息，请参阅[升级和安装常见问题](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)。 
  
## <a name="see-also"></a>另请参阅  
 [R Services 安装问题疑难解答](http://msdn.microsoft.com/library/ce6b902b-a4fa-4b0a-ac0d-be47a59c2a78)  
  
  

