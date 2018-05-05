---
title: sp_redirect_publisher (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2017
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
- sp_redirect_publisher_TSQL
- sp_redirect_publisher
helpviewer_keywords:
- sp_redirect_publisher
ms.assetid: af45e2b2-57fb-4bcd-a58b-e61401fb3b26
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e8df59d709ef04d94626ac2ab6a3ba268d63ab76
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spredirectpublisher-transact-sql"></a>sp_redirect_publisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  为现有发布服务器/数据库对指定重定向的发布服务器。 如果发布服务器数据库属于 Alwayson 可用性组，则重定向发布服务器是与可用性组关联的可用性组侦听器名称。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_redirect_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name'   
    [ , [ @redirected_publisher = ] 'new_publisher' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@original_publisher** =] *****original_publisher*****  
 最初发布数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。 *original_publisher*是**sysname**，无默认值。  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 要发布的数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [ **@redirected_publisher** =] *****redirected_publisher*****  
 与将成为新发布服务器的可用性组相关联的可用性组侦听器名称。 *redirected_publisher*是**sysname**，无默认值。 将可用性组侦听器配置到非默认端口时，请随侦听器名称一并指定端口号，如 `'Listenername,51433'`  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 **sp_redirect_publisher**用于允许复制发布服务器重定向到当前主副本的 Always On 可用性组通过将与可用性组的侦听器关联的发布服务器/数据库对。 执行**sp_redirect_publisher**已为包含已发布的数据库的可用性组配置了可用性组侦听器后。  
  
 如果从可用性组主副本上删除原始发布服务器上的发布数据库，则执行**sp_redirect_publisher**而无需指定的值*@redirected_publisher*若要删除的发布服务器/数据库对的重定向的参数。 有关重定向发布服务器的详细信息时，请参阅[维护 AlwaysOn 发布数据库&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md)。  
  
## <a name="permissions"></a>权限  
 调用方必须要么是的成员**sysadmin**固定服务器角色、 **db_owner**固定的数据库角色的分发数据库中或定义发布一个发布访问列表的成员与发布服务器数据库。  
  
## <a name="see-also"></a>另请参阅  
 [复制存储过程 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
