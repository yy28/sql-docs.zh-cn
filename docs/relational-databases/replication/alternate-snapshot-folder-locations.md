---
title: 备用快照文件夹位置 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], alternate folder locations
- snapshot replication [SQL Server], alternate folder locations
- alternate snapshot folders [SQL Server replication]
ms.assetid: 437553b0-19df-4522-8f27-06b5bc747c69
caps.latest.revision: 36
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 22923e3c7f5cc561e9bd5186bcf3caf2e2a2c9c5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32955902"
---
# <a name="alternate-snapshot-folder-locations"></a>备用快照文件夹位置
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  通过使用备用快照位置，可以将快照文件存储在默认位置以外的位置，默认位置通常在分发服务器上。 备用位置可以在另一台服务器、网络驱动器或可移动介质（如 CD-ROM 或可移动磁盘）上。  
  
 备用快照位置存储为发布的一项属性。 因为备用快照位置是一项发布属性，所以分发代理和合并代理在同步处理的过程中就能定位适当的快照。  
  
 如果要指定一个备用快照文件夹位置或压缩快照文件，请创建发布但不立即创建初始快照，为该快照位置设置发布属性，然后为该发布运行快照代理。 如果在创建初始快照后更改了备用位置，则为该发布生成的任何快照的位置都不会重定位到新的备用位置。 在这种情况下，根据发布设置的不同，合并代理或分发代理可能找不到新备用位置的快照文件。  
  
> [!NOTE]  
>  请不要（使用“发布属性”对话框或 [sp_changepublication (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)）指定与默认快照文件夹位置相同的备用位置。  
  
> [!CAUTION]  
>  不要同时使用 WebSync 和备用快照文件夹位置。  
  
 **指定备用快照位置**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]：[指定备用快照文件夹位置 (SQL Server Management Studio)](../../relational-databases/replication/publish/specify-an-alternate-snapshot-folder-location-sql-server-management-studio.md)  
  
-   复制 [!INCLUDE[tsql](../../includes/tsql-md.md)] 编程：[配置快照属性&#40;复制 Transact-SQL 编程&#41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用快照初始化订阅](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [快照选项](../../relational-databases/replication/snapshot-options.md)  
  
  
