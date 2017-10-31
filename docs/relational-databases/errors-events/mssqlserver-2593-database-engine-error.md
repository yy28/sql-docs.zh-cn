---
title: MSSQLSERVER_2593 | Microsoft Docs
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
- 2593 (Database Engine error)
ms.assetid: 2e25bc43-606a-40de-8b87-3b55b96f4a91
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0a9bdc92a62edb40e929e9d7bcbcff172e161187
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver2593"></a>MSSQLSERVER_2593
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2593|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_OBJECT_ROW_PAGE_SUMMARY|  
|消息正文|对象 'object' 的 PAGECOUNT 页中有 ROWCOUNT 行。|  
  
## <a name="explanation"></a>解释  
此消息是所有 DBCC 检查（DBCC CHECKALLOC 除外）返回的信息性输出的一部分，指示指定对象的行和页计数。  
  
## <a name="user-action"></a>用户操作  
InclusionThresholdSetting  
  

