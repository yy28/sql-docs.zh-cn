---
title: MSSQLSERVER_41342 | Microsoft Docs
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
- 41342 (Database Engine error)
ms.assetid: 28270d98-c543-4e7d-b40c-2200e38dce1c
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f1a90ed7be17639664707cded4f752ba629b6421
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver41342"></a>MSSQLSERVER_41342
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41342|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|HK_HW_NOT_SUPPORTED|  
|消息正文|系统上的处理器型号不支持创建 *construct*。 较早的处理器通常会出现此错误。 有关支持的型号的信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书。|  
  
## <a name="explanation"></a>解释  
内存优化的表要求处理器型号支持对 128 位值执行原子比较和交换操作，这要求装配说明 CMPXCHG16B。 一些较旧的 AMD 处理器型号不支持 CMPXCHG16B 指令。 此外，默认情况下，某些虚拟化环境不启用此指令。  
  
## <a name="user-action"></a>用户操作  
升级您的处理器。 如果您的处理器支持该指令并且您正在虚拟机中运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则更改配置以便支持指令 CMPXCHG16B。  
  
## <a name="see-also"></a>另请参阅  
[内存中 OLTP（内存中优化）](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  

