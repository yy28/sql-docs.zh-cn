---
description: sp_delete_proxy (Transact-SQL)
title: sp_delete_proxy (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_proxy
- sp_delete_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_proxy
- DROP PROXY statement
ms.assetid: 44a1db13-b7f2-4dab-a1b5-b8dafb41737c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ccc9d7639bbe7f929a28b249e6767d0d703a0068
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89528876"
---
# <a name="sp_delete_proxy-transact-sql"></a>sp_delete_proxy (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  删除指定代理。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_delete_proxy [ @proxy_id = ] id , [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>参数  
`[ @proxy_id = ] id` 要删除的代理的代理标识号。 *Proxy_id*的值为**int**，默认值为 NULL。  
  
`[ @proxy_name = ] 'proxy_name'` 要删除的代理的名称。 *Proxy_name*的值为**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或 **1** (失败)   
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>备注  
 必须指定** \@ proxy_name**或** \@ proxy_id** 。 如果同时指定这两个参数，这两个参数必须引用相同的代理，否则存储过程会失败。  
  
 如果作业步骤引用了指定代理，则无法删除此代理，存储过程也将失败。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才能 **sp_delete_proxy**执行。  
  
## <a name="examples"></a>示例  
 以下是删除代理 `Catalog application proxy` 的示例。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_proxy  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_proxy &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)  
  
  
