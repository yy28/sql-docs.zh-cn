---
title: "即时文件初始化配置 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58be8982-4d2e-4aa3-bcdd-874a062d2f9d
caps.latest.revision: "20"
ms.openlocfilehash: b7dda4bb925e08f49409ea1950cfe3649b4db3e0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="instant-file-initialization-configuration"></a>即时文件初始化配置
即时文件初始化功能允许数据文件操作更快地运行 SQL Server 功能。 选中的复选框，以开启即时文件初始化会提高性能的 SQL Server PDW。 但是，如果这会带来安全风险为你的业务，然后选中框。  
  
> [!IMPORTANT]  
> 启用即时文件初始化后，SQL Server 不会用零覆盖已删除的位。  如果未经授权的用户获得访问权限已删除的数据，此行为可以创建一个安全漏洞。 但是，SQL Server PDW 缓解此风险通过确保 SQL Server 数据库和备份文件总是附加到 SQL Server; 的实例只有 SQL Server 服务帐户和本地管理员可以访问 SQL Server PDW 上的已删除的数据。  
  
当启用 TDE 时，即时文件初始化功能不可用。  
  
## <a name="add-permission-for-the-backup-account"></a>添加为备份的帐户的权限  
备份过程需要可以访问的备份存储位置的网络凭据 （Windows 用户帐户）。 授权 PDW 通过使用使用帐户[sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)过程。 请参阅[备份数据库](../t-sql/statements/backup-database-parallel-data-warehouse.md)为整个备份过程。 若要使用即时文件初始化，必须为备份的帐户授予`Perform volume maintenance tasks`权限。  
  
1.  在备份服务器上，打开**本地安全策略**应用程序 (`secpol.msc`)。  
  
2.  在左侧窗格中，展开“本地策略” ，然后单击“用户权限指派” 。  
  
3.  在右侧窗格中，双击“执行卷维护任务”。  
  
4.  单击“添加用户或组”  ，添加用于备份的任何用户帐户。  
  
5.  单击“应用” ，然后关闭所有“本地安全策略”  对话框。  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>若要打开或关闭的即时文件初始化  
  
1.  启动 Configuration Manager。 有关详细信息，请参阅[启动 Configuration Manager &#40;分析平台系统 &#41;](launch-the-configuration-manager.md).  
  
2.  在配置管理器的左窗格中，单击**即时文件初始化**。  
  
3.  若要启用即时文件初始化，选中框旁边**所有节点上启用即时文件初始化**。 要关闭即时文件初始化，请清除此框旁边**所有节点上启用即时文件初始化**。  
  
    > [!WARNING]  
    > 时关闭即时文件初始化，上述功能的安全性注意事项可能仍将应用于启用即时文件初始化的同时删除的文件中。  
  
4.  单击 **“应用”**。 下次重启设备服务，更改将传播到整个 SQL Server PDW 上的 SQL Server 实例。 若要立即重新启动设备服务，请参阅[PDW 服务状态 &#40;分析平台系统 &#41;](pdw-services-status.md).  
  
5.  你可能需要重复为上面所述的步骤**备份帐户添加权限**删除**执行卷维护任务**权限。  
  
![DWConfig 设备 PDW 即时文件初始化](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
有关即时文件初始化的详细信息，请参阅[即时文件初始化](http://technet.microsoft.com/en-us/library/ms175935(v=SQL.105).aspx)。  
  
