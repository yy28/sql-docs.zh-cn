---
title: "sp_check_dynamic_filters (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 096c6ff70b712b283191afeddbb7e9d9c6afd36a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spcheckdynamicfilters-transact-sql"></a>sp_check_dynamic_filters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示有关发布的参数化行筛选器属性的信息，特别是用于为发布生成已筛选数据分区的函数以及关于发布是否有资格使用预计算分区的信息。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_check_dynamic_filters [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication** =] *发布*  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|是使用预计算的分区; 如果限定发布其中**1**意味着，可以使用分区，预计算和**0**意味着不能使用。|  
|**has_dynamic_filters**|**bit**|是中发布; 定义了至少一个参数化的行筛选器其中**1**意味着存在一个或多个参数化的行筛选器，和**0**意味着存在任何动态筛选器。|  
|**dynamic_filters_function_list**|**nvarchar(500)**|用于对发布中的项目进行筛选的函数列表，各个函数由分号分隔。|  
|**validate_subscriber_info**|**nvarchar(500)**|用于对发布中的项目进行筛选的函数列表，各个函数由加号 (+) 分隔。|  
|**uses_host_name**|**bit**|如果[host_name （)](../../t-sql/functions/host-name-transact-sql.md)函数使用在参数化的行筛选器，其中**1**意味着对动态筛选使用此函数。|  
|**uses_suser_sname**|**bit**|如果[suser_sname （)](../../t-sql/functions/suser-sname-transact-sql.md)函数使用在参数化的行筛选器，其中**1**意味着对动态筛选使用此函数。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_check_dynamic_filters**合并复制中使用。  
  
 如果发布被定义为使用预计算的分区， **sp_check_dynamic_filters**检查预计算分区的任何的限制冲突。 如果发现任何这类情况，则将返回错误。 有关详细信息，请参阅[使用预计算分区优化参数化筛选器性能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
 如果已将发布定义为具有参数化行筛选器，但未找到参数化行筛选器，则将返回错误。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_check_dynamic_filters**。  
  
## <a name="see-also"></a>另请参阅  
 [为参数化筛选器与合并发布管理分区](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [sp_check_join_filter &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-check-join-filter-transact-sql.md)   
 [sp_check_subset_filter &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-check-subset-filter-transact-sql.md)  
  
  
