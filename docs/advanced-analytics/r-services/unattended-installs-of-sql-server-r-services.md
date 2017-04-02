---
title: "SQL Server R Services 的无人参与安装 | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 14
---
# SQL Server R Services 的无人参与安装
    
在开始之前安装过程，请注意这些要求︰

+ 你必须在安装将在其中使用 R 服务 （数据库） 的每个实例上的数据库引擎 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
+ 如果您正在执行脱机安装，必须提前，下载所需的 R 组件并将它们复制到本地文件夹。 有关下载位置，请参阅 [没有 Internet 访问权限安装 R 组件](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)。   
+ 没有新的参数， */IACCEPTROPENLICENSETERMS*, ，指示已接受使用开放源代码 R 组件的许可条款。 如果在命令行中不包括此参数，则安装将失败。  
  
## 执行 R Services (In-Database) 的无人参与安装  
 下面的示例演示要执行静默、 无人参与安装 R 中的服务时在命令行中指定的最小所需的功能 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
###  <a name="bkmk_Unattended"></a>  
  
1.  从提升的命令提示符运行以下命令︰  
  
    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,AdvancedAnalytics /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS  
    ```  
  
2.  完成安装之后，先在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中运行以下命令以启用该功能。  
  
    ```  
    Exec sp_configure  'external scripts enabled', 1  
    Reconfigure  with  override  
  
    ```  
  
    > [!NOTE]  
    >  你必须显式启用引擎功能；否则，它将无法调用 R 脚本，即使安装程序已安装并配置该功能也是如此。  
  
3.  重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 此操作也会自动重启相关的 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务。  
  
## 另请参阅  
 [R Services 安装程序故障排除](../Topic/Troubleshooting%20R%20Services%20Setup.md)  
  
  