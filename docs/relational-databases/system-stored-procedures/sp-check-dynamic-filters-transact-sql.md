---
title: sp_check_dynamic_filters (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- dynamic_filters_TSQL
- sp_check_TSQL
- check
- sp_check_dynamic filter
- check_TSQL
- filters_TSQL
- check_dynamic_filters_TSQL
- dynamic filters
- filters
- check dynamic filters
- sp_check_dynamic filter_TSQL
- sp_check_for_sync_trigger_TSQL
- sp_check
helpviewer_keywords:
- sp_check_dynamic_filters
ms.assetid: dd7760db-a3a5-460f-bd97-b8d436015e19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 498d9573ce7c70d4ec96ffe01d34d3756335cf0f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718725"
---
# <a name="spcheckdynamicfilters-transact-sql"></a>sp_check_dynamic_filters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示有关发布的参数化行筛选器属性的信息，特别是用于为发布生成已筛选数据分区的函数以及关于发布是否有资格使用预计算分区的信息。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_check_dynamic_filters [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication** =] **'***发布*****  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|是发布是否限定使用预计算的分区;其中**1**意味着，可以使用分区，预计算并**0**意味着不能使用它们。|  
|**has_dynamic_filters**|**bit**|如果已发布; 中定义至少一个参数化的行筛选器其中**1**意味着存在一个或多个参数化的行筛选器，并**0**意味着存在任何动态筛选器。|  
|**dynamic_filters_function_list**|**nvarchar(500)**|用于对发布中的项目进行筛选的函数列表，各个函数由分号分隔。|  
|**validate_subscriber_info**|**nvarchar(500)**|用于对发布中的项目进行筛选的函数列表，各个函数由加号 (+) 分隔。|  
|**uses_host_name**|**bit**|如果[host_name （)](../../t-sql/functions/host-name-transact-sql.md)函数用在参数化的行筛选器，其中**1**表示此函数使用了动态筛选。|  
|**uses_suser_sname**|**bit**|如果[suser_sname （)](../../t-sql/functions/suser-sname-transact-sql.md)函数用在参数化的行筛选器，其中**1**表示此函数使用了动态筛选。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_check_dynamic_filters**合并复制中使用。  
  
 如果将发布定义以使用预计算的分区**sp_check_dynamic_filters**检查任何违反行为的预计算分区的限制。 如果发现任何这类情况，则将返回错误。 有关详细信息，请参阅[使用预计算分区优化参数化筛选器性能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
 如果已将发布定义为具有参数化行筛选器，但未找到参数化行筛选器，则将返回错误。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_check_dynamic_filters**。  
  
## <a name="see-also"></a>请参阅  
 [参数化筛选器为合并发布管理分区](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [sp_check_join_filter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-check-join-filter-transact-sql.md)   
 [sp_check_subset_filter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-check-subset-filter-transact-sql.md)  
  
  
