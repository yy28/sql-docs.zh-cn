---
description: sp_mergedummyupdate (Transact-SQL)
title: sp_mergedummyupdate (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergedummyupdate_TSQL
- sp_mergedummyupdate
helpviewer_keywords:
- sp_mergedummyupdate
ms.assetid: b834f7f6-9588-4d59-a3e2-83d8e8e722e1
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dbacf385842d226c733c5c1baec9859f26e140d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464126"
---
# <a name="sp_mergedummyupdate-transact-sql"></a>sp_mergedummyupdate (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  在给定的行中进行虚更新，以便在下次合并时将该行再次发送。 此存储过程可在发布服务器的发布数据库中执行或在订阅服务器的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_mergedummyupdate [ @source_object =] 'source_object', [ @rowguid =] 'rowguid'  
```  
  
## <a name="arguments"></a>参数  
`[ @source_object = ] 'source_object'` 源对象的名称。 *source_object*为 **nvarchar (386) **，无默认值。  
  
`[ @rowguid = ] 'rowguid'` 行标识符。 *rowguid* 是 **uniqueidentifier**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或 **1** (失败)   
  
## <a name="remarks"></a>备注  
 **sp_mergedummyupdate** 用于合并复制。  
  
 如果你编写自己的复制冲突查看器 ( # A0) ， **sp_mergedummyupdate**会很有用。  
  
## <a name="permissions"></a>权限  
 只有 **db_owner** 固定数据库角色的成员才能执行 **sp_mergedummyupdate**。  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
