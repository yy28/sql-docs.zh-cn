---
title: 在故障转移群集中设置 FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], setting up on a failover cluster
ms.assetid: 6721f780-20b7-4109-8ddb-ac327310699e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 23205cf2a595b4acb861f6dd5aace217a49a4e2d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47700195"
---
# <a name="set-up-filestream-on-a-failover-cluster"></a>在故障转移群集中设置 FILESTREAM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题说明了如何在故障转移群集中启用 FILESTREAM。 在尝试执行此过程之前，您应该先了解 [故障转移群集](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md) 并启用 FILESTREAM。 有关如何启用 FILESTREAM 的信息，请参阅 [启用和配置 FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)。  
  
### <a name="to-set-up-filestream-on-a-failover-cluster"></a>在故障转移群集中设置 FILESTREAM  
  
1.  为故障转移群集设置主节点。  
  
     在设置完成后，使用 **“SQL Server  配置管理器”** 在主节点上启用 FILESTREAM。 这将启用需要 Windows 管理员特权的设置。 如果需要远程访问，请选择 **“允许远程客户端针对 FILESTREAM 数据启用流访问”**。 这会创建一个文件共享群集资源。  
  
2.  设置被动节点。  
  
     在设置完成后，使用 **“SQL Server 配置管理器”** 在被动节点上启用 FILESTREAM。 在群集的所有节点中，为 **“Windows 共享名”** 指定的名称必须是相同的。  
  
3.  若要添加更多的被动节点，请重复步骤 2。  
  
4.  在添加了所有节点后，在每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例上执行 sp_configure 存储过程以完成该过程。  
  
5.  若要随时在群集中添加并启用其他节点，您可以重复步骤 2、3 和 4。  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [创建新的 SQL Server 故障转移群集（安装程序）](../../sql-server/failover-clusters/install/create-a-new-sql-server-failover-cluster-setup.md)   
 [删除 SQL Server 故障转移群集实例（安装程序）](../../sql-server/failover-clusters/install/remove-a-sql-server-failover-cluster-instance-setup.md)   
 [在 SQL Server 故障转移群集中添加或删除节点（安装程序）](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
  
