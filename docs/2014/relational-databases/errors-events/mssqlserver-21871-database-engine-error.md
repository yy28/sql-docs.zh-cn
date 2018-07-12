---
title: MSSQLSERVER_21871 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 37e4c950488f3cb878e5598eef2a49843e1e36f1
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37421456"
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
 `sp_validate_replica_hosts_as_publishers` 检查 MSredirected_publishers 表分发数据库中的标识的发布服务器和发布服务器数据库的条目。  如果未找到条目，则 `sp_validate_replica_hosts_as_publishers` 返回错误 21871。  
  
## <a name="user-action"></a>用户操作  
 `sp_validate_replica_hosts_as_publishers` 仅与重定向发布服务器有关。 如果发布服务器数据库为可用性组的成员，则使用存储过程 `sp_redirect_publisher` 将发布服务器和发布服务器数据库与可用性组的可用性组侦听器名称关联。  
  
  
