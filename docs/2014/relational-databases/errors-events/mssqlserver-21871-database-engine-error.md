---
title: MSSQLSERVER_21871 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f26211da21829a0a898dfb36ff9fefd453c7ad44
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85034646"
---
# <a name="mssqlserver_21871"></a>MSSQLSERVER_21871
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|21871|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum21871|  
|消息正文|发布服务器“%s”（属于数据库“%s”）尚未重定向。|  
  
## <a name="explanation"></a>说明  
 `sp_validate_replica_hosts_as_publishers` 在分发数据库中检查 MSredirected_publishers 表，以查看是否存在与标识的发布服务器和发布服务器数据库对应的条目。  如果未找到条目，则 `sp_validate_replica_hosts_as_publishers` 返回错误 21871。  
  
## <a name="user-action"></a>用户操作  
 `sp_validate_replica_hosts_as_publishers` 仅与重定向发布服务器有关。 如果发布服务器数据库为可用性组的成员，则使用存储过程 `sp_redirect_publisher` 将发布服务器和发布服务器数据库与可用性组的可用性组侦听器名称关联。  
  
  
