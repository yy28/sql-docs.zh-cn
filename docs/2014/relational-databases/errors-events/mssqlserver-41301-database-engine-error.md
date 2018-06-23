---
title: MSSQLSERVER_41301 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 41301 (Database Engine error)
ms.assetid: c6127e1e-2846-4ee9-bc42-2d896ea9730e
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b40714a2d2aff7a2a7367330c79a50a68321b86c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128766"
---
# <a name="mssqlserver41301"></a>MSSQLSERVER_41301
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41301|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|COMMIT_DEPENDENCY_FAILURE|  
|消息正文|当前事务所依赖的前一事务已终止，当前事务无法再提交。|  
  
## <a name="explanation"></a>解释  
 事务遇到依赖关系错误，已失败。  
  
 依赖事务太多也可导致此错误。 任何写事务的依赖事务都有数量限制。 例如，如果太多的读事务尝试依赖更新事务，就可能会发生此错误。  
  
## <a name="user-action"></a>用户操作  
 不必对事务执行任何操作。 调用 ROLLBACK TRAN 回滚事务。 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>请参阅  
 [启用和禁用 AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
  