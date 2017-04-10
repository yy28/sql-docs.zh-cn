---
title: "修改 SQL Server R 服务的用户帐户池 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 58b79170-5731-46b5-af8c-21164d28f3b0
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# 修改 SQL Server R 服务的用户帐户池
  作为安装过程的一部分 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，新的 Windows *用户帐户池* 创建以支持通过任务的执行 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务。 这些工作人员帐户的目的是隔离的 R 脚本由不同的 SQL 用户并发执行。
  
  该池中用户帐户的数量决定了可同时有多少 R 会话处于活动状态。   如果同一用户同时执行多个 R 脚本，所有这些会话运行由该用户将使用相同的工作帐户。 因此，单个用户可能必须运行并发，只要资源允许的 100 不同 R 脚本。

## 默认配置   
-   在默认情况下，组名称是 **SQLRUserGroup**。 
-   在命名实例中，默认的组名称作为后缀，实例名称︰ 例如， **SQLRUserGroupMyInstanceName**。 
-   帐户︰ 默认情况下，用户帐户池包含 20 个用户帐户，名为 **MSSQLSERVER01** 通过 **MSSQLSERVER20** 对于默认实例。  
-   对于命名实例，使用实例名称命名的用户帐户︰ 例如， **MyInstanceName01** 通过 **MyInstanceName20**。  


## 管理用户组的每个实例
通过创建 Windows 帐户组 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的安装程序在其上 R 已安装服务，因此，如果你已安装支持 R 的多个实例，将多个用户组每个实例。
但是，与每个用户组 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务上的特定实例，并且无法支持其他实例运行的 R 作业。

默认情况下，组执行的操作 **不** 具有登录权限 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 与之关联的实例。 如果你需要能够执行 R 脚本的用户，数据库管理员必须提供此组具有 **连接到** 权限。  

### 更改 Windows 用户组中的工作人员帐户的数量

若要修改的帐户池中的用户数，您必须编辑的属性 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务按如下所述。  
  
与每个用户帐户相关联的密码生成的随机，但你可以在以后更改创建帐户后它们。  
  
1. 打开 SQL Server 配置管理器，然后选择 **SQL Server 服务**。
2. 双击 SQL Server 快速启动板服务并运行时将其停止该服务。 
3.  在 **服务** 选项卡上，请确保启动模式设置为自动。 如果未在运行快速启动板，R 脚本将失败。
4.  单击 **高级** 选项卡上，编辑的值 **外部的用户计数** 如有必要。 此设置可控制多少不同的 SQL 用户可以同时运行查询，在。默认值为 20 个帐户，这在大多数情况下是多个足够用来支持 R 会话。
5. （可选） 可以设置选项 **重置外部用户密码** 到 _是_ 如果您的组织有要求更改密码每隔 90 天的策略。 执行此操作将重新生成加密快速启动板维护用户帐户的密码。    
6.  重新启动服务。  

## 远程脚本执行所需的其他权限
如果您执行与作为远程 SQL Server 计算机的 R 脚本计算上下文，该辅助角色组需要登录到将运行 R 脚本的 SQL Server 实例的权限。

有关详细信息，请参阅 [升级和安装常见问题](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)。 

  
## 另请参阅  
 [配置 (SQL Server R Services)](../../advanced-analytics/r-services/configuration-sql-server-r-services.md)
  