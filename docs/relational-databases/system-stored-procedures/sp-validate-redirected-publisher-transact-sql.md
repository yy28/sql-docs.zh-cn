---
title: "sp_validate_redirected_publisher (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_validate_redirected_publisher
- sp_validate_redirected_publisher_TSQL
helpviewer_keywords: sp_validate_redirected_publisher
ms.assetid: 2b7fdbad-17e4-4442-b0b2-9b5e8f84b91d
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bafe71c88b5fc47c822275ebfb9be102db65b22b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spvalidateredirectedpublisher-transact-sql"></a>sp_validate_redirected_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  验证要发布数据库的当前主机是否有能力支持复制。 必须从分发数据库运行。 此过程称为**sp_get_redirected_publisher**。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
      sp_validate_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>参数  
 [  **@original_publisher**  =] *original_publisher*  
 最初发布数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。 *original_publisher*是**sysname**，无默认值。  
  
 [  **@publisher_db**  =] *publisher_db*  
 要发布的数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [  **@redirected_publisher**  =] *redirected_publisher*  
 重定向的目标时指定**sp_redirect_publisher**为发布服务器/数据库对调用。 *redirected_publisher*是**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 无。  
  
## <a name="remarks"></a>注释  
 如果未输入任何发布服务器和发布数据库， **sp_validate_redirected_publisher**返回输出参数中的 null  *@redirected_publisher* 。 如果存在条目，则在成功和失败的情况下都会在输出参数中返回条目。  
  
 如果验证成功， **sp_validate_redirected_publisher**返回的成功指示。  
  
 如果验证失败，则会引发描述失败的错误。  
  
## <a name="permissions"></a>Permissions  
 调用方必须要么是的成员**sysadmin**固定服务器角色、 **db_owner**固定的数据库角色的分发数据库中或定义发布一个发布访问列表的成员与发布服务器数据库。  
  
## <a name="see-also"></a>另请参阅  
 [复制存储过程 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
