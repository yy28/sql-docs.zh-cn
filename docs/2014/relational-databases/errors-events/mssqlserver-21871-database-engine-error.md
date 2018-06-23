---
title: MSSQLSERVER_21871 | Microsoft Docs
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
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 910fc06aac87eb846c0db76956eb45377fa3ecdb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025934"
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
 `sp_validate_replica_hosts_as_publishers` 检查表 MSredirected_publishers 标识发布服务器和发布服务器数据库的条目的分发数据库中。  如果未找到条目，则 `sp_validate_replica_hosts_as_publishers` 返回错误 21871。  
  
## <a name="user-action"></a>用户操作  
 `sp_validate_replica_hosts_as_publishers` 仅与重定向发布服务器有关。 如果发布服务器数据库为可用性组的成员，则使用存储过程 `sp_redirect_publisher` 将发布服务器和发布服务器数据库与可用性组的可用性组侦听器名称关联。  
  
  