---
title: 配置分析平台系统的即时文件初始化-|Microsoft Docs
description: 在分析平台系统上配置即时文件初始化。 即时文件初始化功能允许数据文件操作，以更快地运行的 SQL Server 功能。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 959d219565de6577e31d9548f5daea0fe0d2419e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298124"
---
# <a name="instant-file-initialization-configuration"></a>即时文件初始化配置
即时文件初始化功能允许数据文件操作，以更快地运行的 SQL Server 功能。 选中的复选框以启用即时文件初始化会提高性能的 SQL Server PDW。 但是，如果这会带来安全风险，业务，然后取消选中框。  
  
> [!IMPORTANT]  
> 启用即时文件初始化后，SQL Server 不会用零覆盖已删除的位。  如果未经授权的用户访问已删除的数据，此行为可以创建一个安全漏洞。 但是，SQL Server PDW 会降低该风险通过确保 SQL Server 数据库和备份文件始终附加到实例的 SQL Server;只有 SQL Server 服务帐户和本地管理员可以访问 SQL Server PDW 上已删除的数据。  
  
当启用 TDE 时，即时文件初始化功能不可用。  
  
## <a name="add-permission-for-the-backup-account"></a>添加备份帐户的权限  
备份过程需要可访问备份存储位置的网络凭据 （Windows 用户帐户）。 授权通过使用帐户的 PDW [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)过程。 请参阅[备份数据库](../t-sql/statements/backup-database-parallel-data-warehouse.md)整个备份过程。 若要使用即时文件初始化，必须授予备份帐户`Perform volume maintenance tasks`权限。  
  
1.  在备份服务器上打开**本地安全策略**应用程序 (`secpol.msc`)。  
  
2.  在左侧窗格中，展开“本地策略”  ，然后单击“用户权限指派”  。  
  
3.  在右侧窗格中，双击“执行卷维护任务”  。  
  
4.  单击“添加用户或组”  ，添加用于备份的任何用户帐户。  
  
5.  单击“应用”  ，然后关闭所有“本地安全策略”  对话框。  
  
## <a name="to-turn-instant-file-initialization-on-or-off"></a>若要启用或禁用即时文件初始化  
  
1.  启动配置管理器。 有关详细信息，请参阅[启动配置管理器&#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)。  
  
2.  在配置管理器的左窗格中，单击**即时文件初始化**。  
  
3.  若要开启即时文件初始化，请选中框旁边**的所有节点上启用即时文件初始化**。 要禁用即时文件初始化，请清除此框旁边**的所有节点上启用即时文件初始化**。  
  
    > [!WARNING]  
    > 当关闭即时文件初始化时，功能上文所述的安全注意事项可能仍适用于启用即时文件初始化的同时删除的文件。  
  
4.  单击 **“应用”** 。 下次重新启动设备服务，更改将传播到整个 SQL Server PDW 上的 SQL Server 实例。 若要立即重新启动设备服务，请参阅[PDW 服务状态&#40;Analytics Platform System&#41;](pdw-services-status.md)。  
  
5.  你可能想要重复作为上面所述的步骤**备份帐户添加权限**若要删除**执行卷维护任务**权限。  
  
![DWConfig 工具 PDW 即时文件初始化](./media/instant-file-initialization-configuration/SQL_Server_PDW_DWConfig_ApplPDWInstant.png "SQL_Server_PDW_DWConfig_ApplPDWInstant")  
  
有关即时文件初始化的详细信息，请参阅[即时文件初始化](https://technet.microsoft.com/library/ms175935(v=SQL.105).aspx)。  
  
