---
title: sp_resyncmergesubscription (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_resyncmergesubscription_TSQL
- sp_resyncmergesubscription
helpviewer_keywords:
- sp_resyncmergesubscription
ms.assetid: e04d464a-60ab-4b39-a710-c066025708e6
author: stevestein
ms.author: sstein
ms.openlocfilehash: e77488a379543dd6f2749a07048fa67a92d530ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041029"
---
# <a name="spresyncmergesubscription-transact-sql"></a>sp_resyncmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将合并订阅重新同步到指定的已知验证状态。 这使您得以将订阅数据库强制集中或同步到特定的时点（如上次成功验证的时间）或指定的日期。 使用此方法重新同步订阅时，不重新应用快照。 此存储过程不用于快照复制订阅或事务复制订阅。 此存储过程在发布服务器的发布数据库中或订阅服务器的订阅数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_resyncmergesubscription [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publisher_db' ]  
        , [ @publication = ] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @resync_type = ] resync_type ]  
    [ , [ @resync_date_str = ] resync_date_string ]  
```  
  
## <a name="arguments"></a>参数  
`[ @publisher = ] 'publisher'` 是发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。 如果存储过程在发布服务器上运行，则 NULL 值有效。 如果在订阅服务器上运行该存储过程，则必须指定发布服务器。  
  
`[ @publisher_db = ] 'publisher_db'` 是发布数据库的名称。 *publisher_db*是**sysname**，默认值为 NULL。 如果存储过程在发布服务器的发布数据库中运行，则 NULL 值有效。 如果在订阅服务器上运行该存储过程，则必须指定发布服务器。  
  
`[ @publication = ] 'publication'` 是发布的名称。 *发布*是**sysname**，无默认值。  
  
`[ @subscriber = ] 'subscriber'` 是订阅服务器的名称。 *订阅服务器上*是**sysname**，默认值为 NULL。 如果存储过程在订阅服务器上运行，则 NULL 值有效。 如果在发布服务器上运行该存储过程，则必须指定订阅服务器。  
  
`[ @subscriber_db = ] 'subscriber_db'` 是订阅数据库的名称。 *subscription_db*是**sysname**，默认值为 NULL。 如果存储过程在订阅服务器的订阅数据库中运行，则 NULL 值有效。 如果在发布服务器上运行该存储过程，则必须指定订阅服务器。  
  
`[ @resync_type = ] resync_type` 定义重新同步的开始处。 *resync_type*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0**|同步从初始快照后开始。 这是占用资源最多的选项，因为自初始快照后的所有更改都重新应用于订阅服务器。|  
|**1**|同步从上次成功验证后开始。 自上次成功验证后发生的所有新的或未完成的生成都重新应用于订阅服务器。|  
|**2**|从中给定的日期开始同步*resync_date_str*。 该日期后发生的所有新的或未完成的生成都重新应用于订阅服务器。|  
  
`[ @resync_date_str = ] resync_date_string` 定义重新同步的开始时的日期。 *resync_date_string*是**nvarchar(30)** ，默认值为 NULL。 使用此参数时*resync_type*的值为**2**。 给定的日期转换为其等效**datetime**值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_resyncmergesubscription**合并复制中使用。  
  
 值为**0**有关*resync_type*参数，它将所有更改重新都应用自初始快照后，可能会占用大量资源，但也许非常少比完全重新初始化。 例如，如果初始快照在一个月前传递，则该值将使得重新应用上个月的数据。 如果初始快照包含 1 GB 的数据，但是在上个月开始的更改量包含 2 MB 的已更改数据，则重新应用数据与重新应用全部 1 GB 快照相比更有效。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_resyncmergesubscription**。  
  
## <a name="see-also"></a>请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
