---
title: MSSQLSERVER_41359 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41359 (Database Engine error)
ms.assetid: 02b717c7-9170-4676-b0f6-4dec9eb5b5d4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b6f71d3c860cb3240195a9877149ee25a58642e2
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551367"
---
# <a name="mssqlserver_41359"></a>MSSQLSERVER_41359
    
## <a name="details"></a>详细信息  
  
|Attribute|值|  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41359|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQL_READ_COMMITTED_SNAPSHOT_NOT_SUPPORTED|  
|消息正文|当数据库选项 READ_COMMITTED_SNAPSHOT 设置为 ON 时，使用 COMMITTED 隔离级别访问内存优化表的查询不能访问基于磁盘的表。 使用表提示（例如 WITH (SNAPSHOT)）为内存优化表提供一种支持的隔离级别。|  
  
## <a name="explanation"></a>说明  
 READ_COMMITTED_SNAPSHOT=ON 的数据库不支持同时访问内存优化表和基于磁盘的表的事务。  
  
## <a name="user-action"></a>用户操作  
 将 READ_COMMITTED_SNAPSHOT 设置为 OFF，或使用表级提示（例如 WITH (SNAPSHOT)）为内存优化表提供一个支持的隔离级别。 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另请参阅  
 [内存中 OLTP（内存中优化）](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
