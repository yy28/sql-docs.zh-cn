---
title: MSSQLSERVER_21871 | Microsoft Docs
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
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1538eba494fcad374dd0454ed519777466317b0f
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver21871"></a>MSSQLSERVER_21871
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|21871|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum21871|  
|消息正文|发布服务器“%s”（属于数据库“%s”）尚未重定向。|  
  
## <a name="explanation"></a>解释  
**sp_validate_replica_hosts_as_publishers** 在分发数据库中检查 MSredirected_publishers 表，以查看是否存在与标识的发布服务器和发布服务器数据库对应的条目。  如果未找到该条目，**sp_validate_replica_hosts_as_publishers** 将返回 21871 错误。  
  
## <a name="user-action"></a>用户操作  
**sp_validate_replica_hosts_as_publishers** 仅适用于重定向的发布服务器。 如果发布服务器数据库为可用性组的成员，则使用存储过程 **sp_redirect_publisher** 将发布服务器和发布服务器数据库与可用性组的可用性组侦听器名称相关联。  
  

