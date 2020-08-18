---
description: MSSQLSERVER_21871
title: MSSQLSERVER_21871 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 52f82fbebc9f164152f6047a90bbb1238e1a2bb7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88332783"
---
# <a name="mssqlserver_21871"></a>MSSQLSERVER_21871
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|21871|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLErrorNum21871|  
|消息正文|发布服务器“%s”（属于数据库“%s”）尚未重定向。|  
  
## <a name="explanation"></a>说明  
**sp_validate_replica_hosts_as_publishers** 在分发数据库中检查 MSredirected_publishers 表，以查看是否存在与标识的发布服务器和发布服务器数据库对应的条目。  如果未找到该条目，**sp_validate_replica_hosts_as_publishers** 将返回 21871 错误。  
  
## <a name="user-action"></a>用户操作  
**sp_validate_replica_hosts_as_publishers** 仅适用于重定向的发布服务器。 如果发布服务器数据库为可用性组的成员，则使用存储过程 **sp_redirect_publisher** 将发布服务器和发布服务器数据库与可用性组的可用性组侦听器名称相关联。  
  
