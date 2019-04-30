---
title: 对 syslockinfo 和 sp_lock 中的行为更改 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- syslockinfo
- sp_lock
ms.assetid: b9892ae3-ac15-48be-8b52-78dbed6467ed
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4e2fa557efb6f09eae78180390c733f35bdc4a17
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63214997"
---
# <a name="changes-to-behavior-in-syslockinfo-and-splock"></a>对 syslockinfo 和 sp_lock 中的行为的更改
  **syslockinfo**并**sp_lock**可能返回意外的值。 它们还可能返回其他行，而以前的版本**syslockinfo**并**sp_lock**返回最多每个锁资源的两个行。  
  
 访问信息从**syslockinfo**或执行**sp_lock**需要对服务器拥有 VIEW SERVER STATE 权限。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 在[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]，则**rsc_objid**并**rsc_indid**中的列**syslockinfo**并**objid**和**indid**中的列**sp_lock**一致地返回的对象 ID 和索引 id。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，可能会返回值 0。  
  
 在中[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]， **syslockinfo**并**sp_lock**在单个事务中返回最多为任何给定的锁资源的两个行。 从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 开始，如果启用了锁分区，就可以针对在一个事务中运行的同一资源返回多行。 那里可能最多 N + 1 行返回，其中 N 是 Cpu 的数目。 另外，现在可以针对同一资源显示 GRANTED 和 WAITING 请求，这在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中是不可能实现的。  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
