---
title: sp_restoredbreplication (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
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
- sp_restoredbreplication
- sp_restoredbreplication_TSQL
helpviewer_keywords:
- sp_restoredbreplication
ms.assetid: a2c5ee32-e6d9-46e9-8031-8ff13c20acf7
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ea73a77c47b4579cda2e97dcea77a8f6516157c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32996984"
---
# <a name="sprestoredbreplication-transact-sql"></a>sp_restoredbreplication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将数据库还原到非发起服务器、数据库或因其他原因而无法运行复制过程的系统时，删除复制设置。 如果将已复制数据库还原到执行备份的服务器或数据库以外的其他服务器或数据库，则将无法保留复制设置。 在恢复时，调用服务器**sp_restoredbreplication**直接以自动从还原的数据库中删除复制元数据。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_restoredbreplication [ @srv_orig = ] 'original_server_name'  
        , [ @db_orig = ] 'original_database_name'  
    [ , [ @keep_replication = ] keep_replication ]  
    [ , [ @perform_upgrade = ] perform_upgrade ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@srv_orig =** ] *****original_server_name*****  
 创建备份的服务器的名称。 *original_server_name*是**sysname**，无默认值。  
  
 [  **@db_orig =** ] *****original_database_name*****  
 已备份数据库的名称。 *original_database_name*是**sysname**，无默认值。  
  
 [  **@keep_replication =** ] *keep_replication*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@perform_upgrade=** ] *perform_upgrade*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_restoredbreplication**在所有类型的复制中使用。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**或**dbcreator**固定的服务器角色或**dbo**数据库架构可以执行**sp_restoredbreplication**.  
  
## <a name="see-also"></a>另请参阅  
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
