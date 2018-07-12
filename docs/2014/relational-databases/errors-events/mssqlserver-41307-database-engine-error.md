---
title: MSSQLSERVER_41307 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 41307 (Database Engine error)
ms.assetid: 56f56410-b07d-4379-b01c-702c95761070
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c7a57b14b0f5b33145c111eb03fed9f5b1fafe46
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429896"
---
# <a name="mssqlserver41307"></a>MSSQLSERVER_41307
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41307|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|HK_HEKATON_ROW_LIMIT|  
|消息正文|已超出了内存优化表 *number* 字节的行大小限制。 请简化表定义。|  
  
## <a name="explanation"></a>解释  
 内存优化表的行大小限制为 8,060 字节。 有关详细信息，请参阅 [内存优化表中的表和行大小](../in-memory-oltp/memory-optimized-tables.md)。 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>请参阅  
 [内存中 OLTP（内存中优化）](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
