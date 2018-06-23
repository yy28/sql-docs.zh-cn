---
title: MSSQLSERVER_12301 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 12301 (Database Engine error)
ms.assetid: 69455df4-4ce9-4a6f-af5a-8bbc93e21245
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fccaee117dfd1203930b633b1c5569ffc67b71f0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025696"
---
# <a name="mssqlserver12301"></a>MSSQLSERVER_12301
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|12301|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|HK_UNSUPPORTED_NULLABLE_COLUMNS|  
|消息正文|“*construct*”不支持索引键中具有可以为 Null 的列。|  
  
## <a name="user-action"></a>用户操作  
 请勿在索引键中使用可以为 Null 的列。  
  
## <a name="see-also"></a>请参阅  
 [内存中 OLTP（内存中优化）](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  