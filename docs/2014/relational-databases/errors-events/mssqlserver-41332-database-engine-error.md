---
title: MSSQLSERVER_41332 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41332 (Database Engine error)
ms.assetid: d3403c3e-d178-4006-b6c9-c18609562db5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0bbd8b256145a9d91e8615aaf7d87a4b8ce7b8b7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62867891"
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
 使用不同的隔离级别启动事务。 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>请参阅  
 [内存中 OLTP（内存中优化）](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
