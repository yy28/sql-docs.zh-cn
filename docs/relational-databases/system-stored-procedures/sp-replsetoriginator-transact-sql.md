---
title: sp_replsetoriginator (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_replsetoriginator
- sp_replsetoriginator_TSQL
helpviewer_keywords:
- sp_replsetoriginator
ms.assetid: 030e5226-0585-439f-b8cd-36f48367d86d
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 680fdf8c36c87549de43825ffd2a7aa5c8fba0f1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32996134"
---
# <a name="spreplsetoriginator-transact-sql"></a>sp_replsetoriginator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用于在双向事务复制中调用环回检测和处理。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_replsetoriginator [ @server_name= ] 'server_name'   
    , [ @database_name= ] 'database_name'  
```  
  
## <a name="arguments"></a>参数  
 [  **@server_name=**] *****server_name*****  
 要应用事务的服务器的名称。 *originating_server*是**sysname**，无默认值。  
  
 [  **@database_name=**] *****database_name*****  
 要应用事务的数据库的名称。 *originating_db*是**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_replsetoriginator**执行由分发代理记录应用复制事务的源。 该信息用于为具有环回属性集的双向事务订阅调用环回检测。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**发布服务器的成员上的固定的服务器角色**db_owner**固定的数据库角色上的发布数据库或在发布访问列表 (PAL) 的用户可以执行**sp_replsetoriginator**。  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
