---
title: sp_get_redirected_publisher (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- sp_get_redirected_publisher_TSQL
- sp_get_redirected_publisher
ms.assetid: d47a9ab5-f2cc-42a8-8be9-a33895ce44f0
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0a2abcc6205929146a37be95fa3943cad1b0ce4d
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43028614"
---
# <a name="spgetredirectedpublisher-transact-sql"></a>sp_get_redirected_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  由复制代理用于查询分发服务器，以确定是否已重定向原始发布服务器。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_get_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @bypass_publisher_validation = ] [0 | 1 ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@original_publisher** =] **'***original_publisher*****  
 要发布的数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 要发布的数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [ **@bypass_publisher_validation** = ] [0 | 1 ]  
 用于绕过重定向的发布服务器的验证。 如果为 0，执行验证。 如果为 1，则不执行验证。 *bypass_publisher_validation*是**位**，默认值为 0。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**redirected_publisher**|**sysname**|重定向后的发布服务器的名称。|  
|**error_number**|**int**|验证错误的错误号。|  
|**error_severity**|**int**|验证错误的严重性。|  
|**error_message**|**nvarchar(4000)**|验证错误消息的文本。|  
  
## <a name="remarks"></a>Remarks  
 *redirected_publisher*返回当前发布服务器名称。 如果发布服务器和发布数据库具有尚未重定向使用，则返回 null **sp_redirect_publisher**。  
  
 如果不请求验证，或如果未输入任何发布服务器和发布数据库中， *error_number*并*error_severity*返回 0 并*error_message*返回 null。  
  
 如果已请求验证，验证存储过程[sp_validate_redirected_publisher &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)调用来验证重定向目标是否适合发布的主机数据库。 如果验证成功， **sp_get_redirected_publisher**返回重定向发布服务器名称，而 0 表示*error_number*并*error_severity*列和中的为 null*error_message*列。  
  
 如果验证请求失败，则会返回重定向的发布服务器的名称以及错误信息。  
  
## <a name="permissions"></a>Permissions  
 调用方必须是的成员**sysadmin**固定服务器角色**db_owner**分发数据库或已定义发布的发布访问列表的成员的固定的数据库角色与发布服务器数据库相关联。  
  
## <a name="see-also"></a>请参阅  
 [复制存储过程 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
