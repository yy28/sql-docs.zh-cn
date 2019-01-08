---
title: sp_getmergedeletetype (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getmergedeletetype
- sp_getmergedeletetype_TSQL
helpviewer_keywords:
- sp_getmergedeletetype
ms.assetid: 64450e4d-844d-4176-874e-f3845536f7d2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ec9d53433d0b06cfc017fde9d312e943a6a3c6d7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52816150"
---
# <a name="spgetmergedeletetype-transact-sql"></a>sp_getmergedeletetype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回合并删除的类型。 该存储过程在发布服务器的发布数据库中或在订阅服务器的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_getmergedeletetype [ @source_object = ] 'source_object', [ @rowguid =] 'rowguid', [ @delete_type=] delete_type OUTPUT  
```  
  
## <a name="arguments"></a>参数  
 [  **@source_object =**] **'***source_object***’**  
 是源对象的名称。 *source_object*是**nvarchar(386)**，无默认值。  
  
 [  **@rowguid=**] **'***rowguid***’**  
 删除类型的行标识符。 *rowguid*是**uniqueidentifier**，无默认值。  
  
 [  **@delete_type=**] *delete_type* **输出**  
 表示删除类型的代码。 *delete_type*是**int**，无默认值。 *delete_type*还是 OUTPUT 参数，并且可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|用户删除|  
|**5**|部分删除|  
|**6**|系统删除|  
  
## <a name="remarks"></a>备注  
 **sp_getmergedeletetype**合并复制中使用。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_getmergedeletetype**。  
  
## <a name="see-also"></a>请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
