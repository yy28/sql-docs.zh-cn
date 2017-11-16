---
title: MSSQLSERVER_17083 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 17083 (Database Engine error)
ms.assetid: 6c83737d-0531-4fd9-88f6-2da5a150532d
caps.latest.revision: "8"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 51d619cd97c294307bf942f1191961dd5a59e8e5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver17083"></a>MSSQLSERVER_17083
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|17083|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|P3_HEKATON_NOT_ATOMIC|  
|消息正文|本机编译存储过程的正文必须是 ATOMIC 块。|  
  
## <a name="explanation"></a>解释  
本机编译存储过程的正文没有 ATOMIC 块。  
  
## <a name="user-action"></a>用户操作  
本机编译存储过程必须包含 ATOMIC 块。 例如：  
  
```  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE= N’us_english’)  
```  
  
有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另请参阅  
[内存中 OLTP（内存中优化）](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
