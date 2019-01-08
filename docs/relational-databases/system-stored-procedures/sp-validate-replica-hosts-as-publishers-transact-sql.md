---
title: sp_validate_replica_hosts_as_publishers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validate_replica_hosts_as_publishers_TSQL
- sp_validate_replica_hosts_as_publishers
helpviewer_keywords:
- sp_validate_replica_hosts_as_publishers
ms.assetid: 45001fc9-2dbd-463c-af1d-aa8982d8c813
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cdbfcad1bb03e88d335c8acddc1ff7eb8c75b2eb
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52791579"
---
# <a name="spvalidatereplicahostsaspublishers-transact-sql"></a>sp_validate_replica_hosts_as_publishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  **sp_validate_replica_hosts_as_publishers**的扩展**sp_validate_redirected_publisher**它允许所有辅助副本进行验证，而不是只是当前主副本。 **sp_validate_replicat_hosts_as_publisher**验证整个 Alwayson 复制拓扑。 **sp_validate_replica_hosts_as_publishers**必须由使用远程桌面会话来避免双跃点安全错误 (21892) 直接在分发服务器上执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_validate_replica_hosts_as_publishers   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>参数  
 [ **@original_publisher** =] **'***original_publisher***’**  
 最初发布数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。 *original_publisher*是**sysname**，无默认值。  
  
 [ **@publisher_db** = ] **'***publisher_db***'**  
 要发布的数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [ **@redirected_publisher** =] **'***redirected_publisher***’**  
 重定向的目标时**sp_redirect_publisher**原始发布服务器/已发布数据库对调用。 *redirected_publisher*是**sysname**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 无。  
  
## <a name="remarks"></a>备注  
 如果未输入任何发布服务器和发布数据库中， **sp_validate_redirected_publisher**返回输出参数为 null *@redirected_publisher*。 否则，在成功和失败的情况下都将返回关联的重定向发布服务器。  
  
 如果验证成功， **sp_validate_redirected_publisher**返回一个成功指示。  
  
 如果验证失败，则会引发相应的错误。  **sp_validate_redirected_publisher**使尽最大努力引发所有问题，而不只是第一个遇到。  
  
> [!NOTE]  
>  在验证不允许读取访问或要求指定读取意图的次要副本主机时，**sp_validate_replica_hosts_as_publishers** 将失败，并显示以下错误。  
>   
>  消息 21899，级别 11，状态 1，过程 **sp_hadr_verify_subscribers_at_publisher**，第 109 行  
>   
>  重定向发布服务器 MyReplicaHostName 用于确定是否有原始发布服务器的订阅服务器的 sysserver 条目处的查询，查询 MyOriginalPublisher 失败，出现错误"976"，错误消息错误 976，级别 14，状态 1，消息：目标数据库 'MyPublishedDB' 参与可用性组和当前不可访问的查询。 数据移动被挂起，或者未启用可用性副本以便用于读访问。 若要允许对该可用性组中的这一数据库和其他数据库进行只读访问，请对组中一个或多个辅助可用性副本启用只读访问权限。  有关详细信息，请参阅 **联机丛书中的** ALTER AVAILABILITY GROUP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语句。  
>   
>  副本主机“MyReplicaHostName”遇到了一个或多个发布服务器验证错误。  
  
## <a name="permissions"></a>权限  
 调用方必须是的成员**sysadmin**固定服务器角色**db_owner**分发数据库或已定义发布的发布访问列表的成员的固定的数据库角色与发布服务器数据库相关联。  
  
## <a name="see-also"></a>请参阅  
 [复制存储过程 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)  
  
  
