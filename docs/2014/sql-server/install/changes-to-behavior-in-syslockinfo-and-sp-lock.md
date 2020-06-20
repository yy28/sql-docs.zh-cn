---
title: Syslockinfo 和 sp_lock 中的行为的更改 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- syslockinfo
- sp_lock
ms.assetid: b9892ae3-ac15-48be-8b52-78dbed6467ed
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 65ace190004cab911dd8996642720620eba94935
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85045161"
---
# <a name="changes-to-behavior-in-syslockinfo-and-sp_lock"></a>对 syslockinfo 和 sp_lock 中的行为的更改
  **syslockinfo**和**sp_lock**可能返回意外值。 它们还可以返回其他行，而以前版本的**syslockinfo**和**sp_lock**每个锁资源最多返回两行。  
  
 若要从**syslockinfo**或执行**sp_lock**中访问信息，需要对服务器具有 VIEW server STATE 权限。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>说明  
 在中 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ，" **syslockinfo** " 和 " **objid** " 中的 " **rsc_indid** **rsc_objid** " 和 " **indid** " 列在**sp_lock**一致地返回对象 id 和索引 id。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，可能会返回值 0。  
  
 在中 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ， **syslockinfo**和**sp_lock**为单个事务中的任何给定的锁资源最多返回两行。 从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 开始，如果启用了锁分区，就可以针对在一个事务中运行的同一资源返回多行。 最多可以返回 N + 1 行，其中 N 是 Cpu 的数目。 另外，现在可以针对同一资源显示 GRANTED 和 WAITING 请求，这在 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中是不可能实现的。  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问 &#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
