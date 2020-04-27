---
title: MSSQL_ENG020596 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020596 error
ms.assetid: fa33627c-2e99-4be3-9424-52ab83446e07
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ddabe3e1a3a12e3aa14c5a6c641345d3236c2fe2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62938477"
---
# <a name="mssql_eng020596"></a>MSSQL_ENG020596
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|20596|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|只有 '%s' 或 db_owner 的成员可以删除匿名代理。|  
  
## <a name="explanation"></a>说明  
 您没有足够的权限删除匿名订阅代理。 调用 [sp_dropanonymousagent (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-dropanonymousagent-transact-sql) 时使用的登录名必须为分发服务器上 **sysadmin** 固定服务器角色的成员或分发数据库中 **db_owner** 固定数据库角色的成员，或者该用户必须是启动该代理首次运行的用户。  
  
## <a name="user-action"></a>用户操作  
 使用适当的凭据登录，并执行 **sp_dropanonymousagent**。  
  
## <a name="see-also"></a>另请参阅  
 [错误和事件参考（复制）](errors-and-events-reference-replication.md)  
  
  
