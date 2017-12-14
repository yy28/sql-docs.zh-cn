---
title: "订阅服务器类型 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newpubwizard.subscribertypes.f1
ms.assetid: a70656cb-21c9-4489-be77-ccd396747e3b
caps.latest.revision: "28"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 514084aeaebdc70ca4f296788aa9b6388119589b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="subscriber-types"></a>订阅服务器类型
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]进行合并发布时可以指定发布必须支持的订阅服务器的类型。 选择订阅服务器类型将会设置“发布兼容级别 ”，该级别可确定发布能够使用哪些功能。  
  
 创建发布快照之后，可以在 **“发布属性”** 对话框的 **“常规”** 页上提高发布兼容级别（使其更为严格）；无法降低兼容级别。  
  
## <a name="options"></a>选项  
 选择此发布必须支持的各个订阅服务器类型。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 该发布可使用所有功能。  
  
 [!INCLUDE[ssEW](../../includes/ssew-md.md)]  
 该发布要求快照文件采用字符格式（由快照代理自动处理）。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 还具有许多与兼容级别无关的限制。  
  
 如果选择了此选项，将为该发布启用 Web 同步选项。 有关 Web 同步的详细信息，请参阅 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)。  
  
## <a name="see-also"></a>另请参阅  
 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [创建发布](../../relational-databases/replication/publish/create-a-publication.md)   
 [查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [属性参考（复制）](../../relational-databases/replication/properties-reference-replication.md)  
  
  
