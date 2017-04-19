---
title: "修改 SQL Server R Services 的用户帐户池 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 58b79170-5731-46b5-af8c-21164d28f3b0
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b45a8ec52fc92f319c150400278fe761723b9ccb
ms.lasthandoff: 04/11/2017

---
# <a name="modify-the-user-account-pool-for-sql-server-r-services"></a>修改 SQL Server R Services 的用户帐户池
  在安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的过程中，将创建一个新的 Windows *用户帐户池*来支持 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务的任务执行。 这些辅助角色帐户的用途是将不同 SQL 用户的 R 脚本并发执行隔离开来。 

本主题介绍辅助角色帐户的默认配置、安全性和容量，以及如何更改默认配置。

## <a name="worker-accounts-used-by-r-services"></a>R Services 使用的辅助角色帐户   

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将为安装 R Services 的每个实例创建 Windows 帐户组。 因此，如果你已安装多个支持 R 的实例，将有多个用户组。

-   在默认实例中，该组的名称为 **SQLRUserGroup**。 
-   在命名的实例中，默认的组名称以实例名称作为后缀：例如 **SQLRUserGroupMyInstanceName**。 

用户帐户池默认包含 20 个用户帐户。 在大多数情况下，20 个帐户足以支持 R 会话，但你也可以更改帐户数目。
-  在默认实例中，各个帐户命名为 **MSSQLSERVER01** 到 **MSSQLSERVER20**。  
-   对于命名的实例，各个帐户根据实例名称命名：例如，**MyInstanceName01** 到 **MyInstanceName20**。  

### <a name = "HowToChangeGroup"></a>如何更改 R 辅助角色帐户的数目

若要修改帐户池中的用户数目，必须按如下所述编辑 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务的属性。  
  
与每个用户帐户关联的密码是随机生成的，但在创建帐户后，你可以更改这些密码。  
  
1. 打开 SQL Server 配置管理器并选择“SQL Server 服务”。
2. 双击 SQL Server Launchpad 服务并停止该服务（如果正在运行）。 
3.  在“服务”选项卡上，确保“启动模式”设置为“自动”。 如果 Launchpad 未运行，R 脚本将会失败。
4.  单击“高级”选项卡，然后根据需要编辑“外部用户计数”的值。 此设置控制有多少个不同的 SQL 用户可在 R 中同时运行查询。默认值为 20 个帐户。
5. （可选）如果组织中的策略要求定期更改密码，可将选项“重置外部用户密码”设置为“是”。 这样，便会重新生成 Launchpad 为用户帐户维护的已加密密码。 有关详细信息，请参阅[实施密码策略](#bkmk_EnforcePolicy)。    
6.  重新启动服务。  

## <a name="managing-r-workload"></a>管理 R 工作负荷

此池中的帐户数目决定了同时有多少 R 会话可处于活动状态。  默认情况下，将创建 20 个帐户，这意味着，20 个不同的用户可以同时创建活动的 R 会话。 如果你预计有更多的并发用户会执行 R 脚本，可以增加辅助角色帐户的数目。 

当同一用户并行执行多个 R 脚本时，该用户运行的所有会话将使用同一个辅助角色帐户。 例如，只要资源允许，单个用户就可以使用单个辅助角色帐户并行运行 100 个不同的 R 脚本。

可支持的辅助角色帐户数以及任何单个用户可运行的并行 R 会话数仅受服务器资源的限制。  通常，在使用 R 运行时时，内存是遇到的第一个瓶颈。

在 R Services 中，R 脚本可以使用的资源受 SQL Server 控制。 我们建议使用 SQL Server DMV 监视资源用量，或者查看关联 Windows 作业对象中的性能计数器，并相应地调整服务器内存用量。 
 
如果你在使用 SQL Server Enterprise Edition，可以通过配置[外部资源池](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md)来分配用于运行 R 脚本的资源。 

有关管理 R 脚本容量的其他信息，请参阅以下文章：

- [R Services 的 SQL Server 配置](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
-  [R Services 的性能案例研究](../../advanced-analytics/r-services/performance-case-study-r-services.md)

## <a name="security"></a>Security

每个用户组都与特定实例上的 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 服务相关联，并且无法支持其他实例上运行的 R 作业。

对于每个辅助角色帐户，当会话处于活动状态时，将创建一个临时文件夹来存储脚本对象、中间结果，以及执行 R 脚本期间 R 和 SQL Server 所用的其他信息。 这些工作文件位于 ExtensibilityData 文件夹中，仅限管理员访问，脚本执行完成后，将由 SQL Server 清除。 

有关详细信息，请参阅[安全概述](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)。

### <a name="bkmk_EnforcePolicy"></a>实施密码策略

如果组织中的某个策略要求定期更改密码，你可能需要强制 Launchpad 服务重新生成 Launchpad 为其辅助角色帐户维护的已加密密码。  

若要启用此设置并强制密码刷新，请在 SQL Server 配置管理器中打开 Launchpad 服务的“属性”窗格，单击“高级”，然后将“重置外部用户密码”更改为“是”。 应用此更改后，将立即为所有用户帐户重新生成密码。 若要在应用此更改后使用 R 脚本，必须重新启动 Launchpad 服务，随后它将会读取新生成的密码。 

若要定期重置密码，可以手动设置此标志或使用脚本。

### <a name="additional-permission-required-to-support-remote-compute-contexts"></a>支持远程计算上下文所需的其他权限

默认情况下，R 辅助角色帐户组对它关联到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例**没有**登录权限。 如果任何 R 用户从远程客户端连接到 SQL Server 来运行 R 脚本，或者脚本使用 ODBC 来获取其他数据，则这种限制可能会造成问题。 

为了确保支持这些方案，数据库管理员必须为 R 辅助角色帐户组提供相应的权限，使其能够登录到要运行 R 脚本的 SQL Server 实例（“连接到”权限）。 这称为*隐含的身份验证*，可让 SQL Server 使用远程用户的凭据运行 R 脚本。

> [!NOTE]
> 如果使用 SQL 登录名从远程工作站运行 R 脚本，则没有此限制，因为 SQL 登录凭据将从 R 客户端显式传递到 SQL Server 实例，再到 ODBC。


### <a name="how-to-enable-implied-authentication"></a>如何启用隐含的身份验证

1. 在运行 R 代码的实例上以管理员身份打开 SQL Server Management Studio。

2. 运行以下脚本。 如果更改了默认值、计算机和实例名称，请务必编辑用户组名称。

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO  
    ````


  
## <a name="see-also"></a>另请参阅  
 [配置 (SQL Server R Services)](../../advanced-analytics/r-services/configuration-sql-server-r-services.md)
  

