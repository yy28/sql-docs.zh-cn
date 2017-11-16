---
title: MSSQLSERVER_5237 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 5237 (Database Engine error)
ms.assetid: 9ff28935-d1eb-47ee-99b3-1a65cb948ce7
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: eafae8fdc25989aaec7ea987d5e72ed7a9221e93
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver5237"></a>MSSQLSERVER_5237
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|5237|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC4_INDEXED_VIEW_CHECK_QUERY_FAILED_NO_ERRORCODE|  
|消息正文|由于内部查询错误，对对象 'NAME' (对象 ID 为 O_ID)进行的 DBCC 跨行集检查失败。|  
  
## <a name="explanation"></a>解释  
因出现内部错误，DBCC 无法通过执行查询来检查索引视图。  
  
## <a name="user-action"></a>用户操作  
重新运行 DBCC 命令。  
  
