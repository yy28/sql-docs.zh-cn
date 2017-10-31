---
title: MSSQLSERVER_7911 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 7911 (Database Engine error)
ms.assetid: dd8390f3-0f77-4fb2-ba94-631a56e42bc6
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: cguyer
robots: noindex,nofollow
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a263211de746ed459a1f76c1146671bb0f746301
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver7911"></a>MSSQLSERVER_7911
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|7911|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC2_REPAIR_PAGE_DEALLOCATED|  
|消息正文|修复：页 P_ID 已从对象 ID O_ID，索引 ID I_ID，分区 ID PN_ID，分配单元 ID A_ID（类型为 TYPE）中释放。|  
  
## <a name="explanation"></a>解释  
这是来自 REPAIR 的信息性消息，指出页已从索引分配映射 (IAM) 页的单页槽数组释放。  
  
## <a name="user-action"></a>用户操作  
InclusionThresholdSetting  
  

