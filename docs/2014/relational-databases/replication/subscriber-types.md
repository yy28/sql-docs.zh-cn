---
title: 订阅服务器类型 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.subscribertypes.f1
ms.assetid: a70656cb-21c9-4489-be77-ccd396747e3b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b9445c7b366a43253da4accabaf98d9c5b7f8d92
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62630640"
---
# <a name="subscriber-types"></a>订阅服务器类型
  进行合并发布时可以指定发布必须支持的订阅服务器的类型。 选择订阅服务器类型将会设置“发布兼容级别  ”，该级别可确定发布能够使用哪些功能。  
  
 创建发布快照之后，可以在 **“发布属性”** 对话框的 **“常规”** 页上提高发布兼容级别（使其更为严格）；无法降低兼容级别。  
  
## <a name="options"></a>选项  
 选择此发布必须支持的各个订阅服务器类型。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 该发布可使用所有功能。  
  
 [!INCLUDE[ssEW](../../includes/ssew-md.md)]  
 该发布要求快照文件采用字符格式（由快照代理自动处理）。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 还具有许多与兼容级别无关的限制。  
  
 如果选择了此选项，将为该发布启用 Web 同步选项。 有关 Web 同步的详细信息，请参阅 [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md)。  
  
## <a name="see-also"></a>另请参阅  
 [发布数据和数据库对象](publish/publish-data-and-database-objects.md)   
 [Create a Publication](publish/create-a-publication.md)   
 [查看和修改分发服务器和发布服务器属性](view-and-modify-distributor-and-publisher-properties.md)   

  
