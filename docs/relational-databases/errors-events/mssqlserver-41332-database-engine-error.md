---
title: MSSQLSERVER_41332 | Microsoft Docs
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
- 41332 (Database Engine error)
ms.assetid: d3403c3e-d178-4006-b6c9-c18609562db5
caps.latest.revision: 7
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: be21e36f47e2bae00387e1f5aed087c94688f930
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver41332"></a>MSSQLSERVER_41332
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41332|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQL_SNAPSHOT_NOT_SUPPORTED|  
|消息正文|当会话 TRANSACTION ISOLATION LEVEL 设置为 SNAPSHOT 时，无法访问或创建内存优化表和本机编译的存储过程。|  
  
## <a name="explanation"></a>解释  
事务在快照隔离级别启动，然后尝试使用不兼容的功能。  
  
## <a name="user-action"></a>用户操作  
使用不同的隔离级别启动事务。 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另请参阅  
[内存中 OLTP（内存中优化）](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  

