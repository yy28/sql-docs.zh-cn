---
title: MSSQLSERVER_17084 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17084 (Database Engine error)
ms.assetid: e579d104-3307-4edd-8587-b14ecbc02ed9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8b3796b97b92c56618e1b9fa98198f83206c825d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48215637"
---
# <a name="mssqlserver17084"></a>MSSQLSERVER_17084
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|17084|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|P3_ATOMIC_WITH_MISSING_OPTION|  
|消息正文|BEGIN ATOMIC 语句的 WITH 子句必须为选项“%ls”指定一个值。|  
  
## <a name="explanation"></a>解释  
 BEGIN ATOMIC 语句的 WITH 子句没有为某一选项指定值。  
  
## <a name="user-action"></a>用户操作  
 `ATOMIC` 块要求为 `WITH` 选项 `TRANSACTION ISOLATION LEVEL` 和 `LANGUAGE` 提供值。 例如：  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N’us_english’)  
```  
  
 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>请参阅  
 [内存中 OLTP（内存中优化）](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
