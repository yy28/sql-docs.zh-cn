---
title: "sp_register_custom_scripting (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_register_custom_scripting
- sp_register_custom_scripting_TSQL
helpviewer_keywords:
- sp_register_custom_scripting
ms.assetid: a8159282-de3b-4b9e-bdc9-3d3fce485c7f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16274b71d1ce14b2a143e5d6ce723bcb64cbaebd
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spregistercustomscripting-transact-sql"></a>sp_register_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  复制允许用户定义的自定义存储过程替换事务复制中使用的一个或多个默认过程。 对复制的表进行架构更改时，将重新创建这些存储过程。 **sp_register_custom_scripting**注册存储的过程或[!INCLUDE[tsql](../../includes/tsql-md.md)]执行架构更改时编写新用户定义自定义存储过程的定义的脚本执行的脚本文件。 这个新的用户定义的自定义存储过程应反映表的新架构。 **sp_register_custom_scripting**在发布服务器上发布数据库中，执行和已注册的脚本文件或存储的过程在订阅服务器上执行时执行架构更改。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_register_custom_scripting [ @type  = ] 'type'  
    [ @value = ] 'value'   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@type**  =] *类型*  
 注册的自定义存储过程或脚本的类型。 *类型*是**varchar(16)**，无默认值，并且可为以下值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**插入**|复制 INSERT 语句时，将执行注册的自定义存储过程。|  
|**更新**|复制 UPDATE 语句时，将执行注册的自定义存储过程。|  
|**删除**|复制 DELETE 语句时，将执行注册的自定义存储过程。|  
|**custom_script**|在数据定义语言 (DDL) 触发器的末尾执行脚本。|  
  
 [  **@value** =] *值*  
 存储过程的名称，或注册的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本文件的名称和完全限定的路径。 *值*是**nvarchar(1024)**，无默认值。  
  
> [!NOTE]  
>  指定 NULL 为*值*参数将注销以前已注册的脚本，这是运行相同[sp_unregister_custom_scripting](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)。  
  
 时的值*类型*是**custom_script**，名称和完整路径[!INCLUDE[tsql](../../includes/tsql-md.md)]预期脚本文件。 否则为*值*必须已注册的存储过程的名称。  
  
 [  **@publication** =] *发布*  
 为其注册自定义存储过程或脚本的发布的名称。 *发布*是**sysname**，默认值为**NULL**。  
  
 [  **@article** =] *文章*  
 为其注册自定义存储过程或脚本的项目的名称。 *文章*是**sysname**，默认值为**NULL**。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_register_custom_scripting**快照和事务复制中使用。  
  
 应在对复制的表进行架构更改前执行此存储过程。 有关使用此存储的过程的详细信息，请参阅[重新生成自定义事务的过程，以反映架构更改](../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md)。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定服务器角色、 **db_owner**固定数据库角色或**db_ddladmin**固定的数据库角色可以执行**sp_register_custom_scripting**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_unregister_custom_scripting &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)  
  
  
