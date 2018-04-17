---
title: sp_validate_replica_hosts_as_publishers (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_validate_replica_hosts_as_publishers_TSQL
- sp_validate_replica_hosts_as_publishers
helpviewer_keywords:
- sp_validate_replica_hosts_as_publishers
ms.assetid: 45001fc9-2dbd-463c-af1d-aa8982d8c813
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d228e234a084057ef69e95b5a6dea69044ffc465
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="spvalidatereplicahostsaspublishers-transact-sql"></a>sp_validate_replica_hosts_as_publishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  **sp_validate_replica_hosts_as_publishers**是的扩展**sp_validate_redirected_publisher** ，它可让所有要验证，而不是只是当前主副本的辅助副本。 **sp_validate_replicat_hosts_as_publisher**验证整个 Always On 复制拓扑。 **sp_validate_replica_hosts_as_publishers**必须通过使用远程桌面会话若要避免双跃点安全错误 (21892) 直接在分发服务器上执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_validate_replica_hosts_as_publishers   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>参数  
 [ **@original_publisher** =] *****original_publisher*****  
 最初发布数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。 *original_publisher*是**sysname**，无默认值。  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 要发布的数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [ **@redirected_publisher** =] *****redirected_publisher*****  
 重定向的目标时**sp_redirect_publisher**调用了原始发布服务器/已发布数据库对。 *redirected_publisher*是**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 无。  
  
## <a name="remarks"></a>注释  
 如果未输入任何发布服务器和发布数据库， **sp_validate_redirected_publisher**返回输出参数为 null *@redirected_publisher*。 否则，在成功和失败的情况下都将返回关联的重定向发布服务器。  
  
 如果验证成功， **sp_validate_redirected_publisher**返回的成功指示。  
  
 如果验证失败，则会引发相应的错误。  **sp_validate_redirected_publisher**使最大努力引发所有问题，而不仅仅在第遇到。  
  
> [!NOTE]  
>  在验证不允许读取访问或要求指定读取意图的次要副本主机时，**sp_validate_replica_hosts_as_publishers** 将失败，并显示以下错误。  
>   
>  消息 21899，级别 11，状态 1，过程 **sp_hadr_verify_subscribers_at_publisher**，第 109 行  
>   
>  重定向的发布服务器“MyReplicaHostName”处的查询失败，该查询用于确定是否有原始发布服务器“MyOriginalPublisher”的订阅服务器的 sysserver 条目，出现错误“976”，错误消息“错误 976，级别 14，状态 1，消息：目标数据库‘MyPublishedDB’正参与某个可用性组，查询当前无法访问该数据库。 数据移动被挂起，或者未启用可用性副本以便用于读访问。 若要允许对该可用性组中的这一数据库和其他数据库进行只读访问，请对组中一个或多个辅助可用性副本启用只读访问权限。  有关详细信息，请参阅 **联机丛书中的** ALTER AVAILABILITY GROUP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语句。  
>   
>  副本主机“MyReplicaHostName”遇到了一个或多个发布服务器验证错误。  
  
## <a name="permissions"></a>权限  
 调用方必须要么是的成员**sysadmin**固定服务器角色、 **db_owner**固定的数据库角色的分发数据库中或定义发布一个发布访问列表的成员与发布服务器数据库。  
  
## <a name="see-also"></a>另请参阅  
 [复制存储过程 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)  
  
  
