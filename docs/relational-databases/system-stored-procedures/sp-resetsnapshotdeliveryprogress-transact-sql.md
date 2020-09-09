---
description: sp_resetsnapshotdeliveryprogress (Transact-SQL)
title: sp_resetsnapshotdeliveryprogress (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_resetsnapshotdeliveryprogress
- sp_resetsnapshotdeliveryprogress_TSQL
helpviewer_keywords:
- sp_resetsnapshotdeliveryprogress
ms.assetid: 5df7d86b-d343-4d9b-88b1-74429ed092e6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b4bcee8dfc47a489fc605bcd3bd787a1ed393329
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543068"
---
# <a name="sp_resetsnapshotdeliveryprogress-transact-sql"></a>sp_resetsnapshotdeliveryprogress (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  重置请求订阅的快照传递进程，以便重新启动快照传递。 在订阅服务器的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_resetsnapshotdeliveryprogress [ [ @verbose_level = ] verbose_level ]  
    [ , [ @drop_table = ] 'drop_table' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @verbose_level = ] verbose_level` 指定返回的信息量。 *verbose_level*的值为 **int**，默认值为 **1**。 如果值为 **1** ，则表示如果无法对 **MSsnapshotdeliveryprogress** 表获取必要的锁，则返回错误， **0** 表示不返回错误。  
  
`[ @drop_table = ] 'drop_table'` 指示是删除还是截断包含有关快照进度信息的表。*drop_table* 为 **nvarchar (5) **，默认值为 **FALSE**。 false 表示截断表，true 表示删除表。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或 **1** (失败)   
  
## <a name="remarks"></a>备注  
 **sp_resetsnapshotdeliveryprogress** 删除 **MSsnapshotdeliveryprogress** 表中的所有行。 这可以在快照传进程中有效的删除由前一进程在订阅数据库中留下的所有元数据。  
  
## <a name="permissions"></a>权限  
 只有 **sysadmin** 固定服务器角色的成员或 **db_owner** 固定数据库角色的成员才能执行 **sp_resetsnapshotdeliveryprogress**。  
  
## <a name="see-also"></a>另请参阅  
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
