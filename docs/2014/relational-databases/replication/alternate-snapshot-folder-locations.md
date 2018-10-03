---
title: 备用快照文件夹位置 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], alternate folder locations
- snapshot replication [SQL Server], alternate folder locations
- alternate snapshot folders [SQL Server replication]
ms.assetid: 437553b0-19df-4522-8f27-06b5bc747c69
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: adcf3258d01d8c6a25a35ae5f802c0a475a6e7bc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133677"
---
# <a name="alternate-snapshot-folder-locations"></a>备用快照文件夹位置
  通过使用备用快照位置，可以将快照文件存储在默认位置以外的位置，默认位置通常在分发服务器上。 备用位置可以在另一台服务器、网络驱动器或可移动介质（如 CD-ROM 或可移动磁盘）上。  
  
 备用快照位置存储为发布的一项属性。 因为备用快照位置是一项发布属性，所以分发代理和合并代理在同步处理的过程中就能定位适当的快照。  
  
 如果要指定一个备用快照文件夹位置或压缩快照文件，请创建发布但不立即创建初始快照，为该快照位置设置发布属性，然后为该发布运行快照代理。 如果在创建初始快照后更改了备用位置，则为该发布生成的任何快照的位置都不会重定位到新的备用位置。 在这种情况下，根据发布设置的不同，合并代理或分发代理可能找不到新备用位置的快照文件。  
  
> [!NOTE]  
>  请不要（使用“发布属性”对话框或 [sp_changepublication (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)）指定与默认快照文件夹位置相同的备用位置。  
  
> [!CAUTION]  
>  不要同时使用 WebSync 和备用快照文件夹位置。  
  
 **指定备用快照位置**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]：[指定备用快照文件夹位置 (SQL Server Management Studio)](publish/specify-an-alternate-snapshot-folder-location-sql-server-management-studio.md) 
  
-   复制 [!INCLUDE[tsql](../../includes/tsql-md.md)] 编程：[配置快照属性&#40;复制 Transact-SQL 编程&#41;](publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>请参阅  
 [使用快照初始化订阅](initialize-a-subscription-with-a-snapshot.md)   
 [快照选项](snapshot-options.md)  
  
  
