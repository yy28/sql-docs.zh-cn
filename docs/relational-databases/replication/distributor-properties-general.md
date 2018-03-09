---
title: "分发服务器属性，常规 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.configdistwizard.distproperties.general.f1
helpviewer_keywords: Distributor Properties dialog box
ms.assetid: ab4120ec-e524-4c0c-8b48-f2f40adb1a3b
caps.latest.revision: "22"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6ca8eee800c47b047b27097ce84a425f1cf251d1
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2018
---
# <a name="distributor-properties-general"></a>分发服务器属性，常规
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]使用“分发服务器属性”对话框的“常规”页，可以添加和删除分发数据库，以及设置分发数据库属性。  
  
 分发数据库用于存储所有类型复制的元数据和历史记录数据，并存储事务复制的事务。 在许多情况下，单个分发数据库就能够满足需要。 不过，如果多个发布服务器使用单个分发服务器，则应考虑为每个发布服务器都创建一个分发数据库。 这样可确保通过每个分发数据库的数据流是不同的。  
  
## <a name="options"></a>“常规”  
 **数据库**  
 **“数据库”** 属性网格显示了分发服务器上分发数据库的名称和保持期属性。 **“事务保持期”** 是指为事务复制存储事务的时间长度（事务保持期也称为分发保持期）。 **“历史记录保持期”** 是指为所有类型的复制存储历史记录元数据的时间长度。 有关分发保持期的详细信息，请参阅[订阅过期和停用](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
 单击**“数据库”**属性网格中的属性按钮 ( **...** ) 可启动 **“分发数据库属性”** 对话框。  
  
 **新建**  
 单击此项可创建一个新的分发数据库。  
  
 **删除**  
 选择 **“数据库”** 属性网格中的一个现有分发数据库，再单击 **“删除”** ，即可删除该数据库。 如果只有一个这样的分发数据库，则无法删除；每个分发服务器必须至少有一个分发数据库。 若要删除所有分发数据库，则必须在该计算机上禁用分发功能。 有关详细信息，请参阅[禁用发布和分发](../../relational-databases/replication/disable-publishing-and-distribution.md)。  
  
 **默认配置文件**  
 单击此项可访问 **“代理配置文件”** 对话框中的复制代理配置文件。 有关配置文件的详细信息，请参阅 [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
## <a name="see-also"></a>另请参阅  
 [“配置分发”](../../relational-databases/replication/configure-distribution.md)   
 [查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)  
  
  
