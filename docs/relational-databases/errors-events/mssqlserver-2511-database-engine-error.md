---
title: MSSQLSERVER_2511 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 2511 (Database Engine error)
ms.assetid: 9a00c0ed-eb4b-4fae-8016-192396006c37
caps.latest.revision: "12"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 4b9527edc01750504d8ad46d0e6a20c53dc94d39
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver2511"></a>MSSQLSERVER_2511
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2511|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_KEYS_OUT_OF_ORDER|  
|消息正文|表错误: 对象 ID %d，索引 ID %d，分区 ID %I64d，分配单元 ID %I64d (类型为 %.*ls)。 页 %S_PGID，槽 %d 和 %d 中的键顺序不对。|  
  
## <a name="explanation"></a>解释  
在指定的索引中检测到顺序不对的键。 包含这些键的页可能已损坏。  
  
## <a name="user-action"></a>用户操作  
使用 ALTER INDEX REBUILD 语句重新生成指定的索引。  
  
