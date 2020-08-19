---
description: DROP REMOTE SERVICE BINDING (Transact-SQL)
title: DROP REMOTE SERVICE BINDING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP REMOTE SERVICE BINDING
- DROP_REMOTE_SERVICE_BINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping remote service bindings
- removing remote service bindings
- deleting remote service bindings
- remote service bindings [Service Broker], dropping
- DROP REMOTE SERVICE BINDING statement
ms.assetid: 377789b4-bf94-488f-8c20-687d0bae447a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f35d18ea74041bf21b1f67010333ff73b3ef808c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444617"
---
# <a name="drop-remote-service-binding-transact-sql"></a>DROP REMOTE SERVICE BINDING (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  删除远程服务绑定。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```syntaxsql
  
DROP REMOTE SERVICE BINDING binding_name  
[ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>参数
 binding_name  
 要删除的远程服务绑定的名称。 不能指定服务器、数据库和架构名称。  
  
## <a name="permissions"></a>权限  
 远程服务绑定的所有者、db_owner 固定数据库角色的成员以及 sysadmin 固定服务器角色的成员默认拥有删除远程服务绑定的权限。  
  
## <a name="examples"></a>示例  
 下面的示例从数据库中删除远程服务绑定 `APBinding`。  
  
```  
DROP REMOTE SERVICE BINDING APBinding ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE REMOTE SERVICE BINDING (Transact-SQL)](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [ALTER REMOTE SERVICE BINDING (Transact-SQL)](../../t-sql/statements/alter-remote-service-binding-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
