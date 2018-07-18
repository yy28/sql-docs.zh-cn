---
title: sp_check_subset_filter (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
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
- sp_check_TSQL
- sp_check_subset_filter
- filter
- subset
- subset_TSQL
- sp_check
- sp_check_subset_filter_TSQL
helpviewer_keywords:
- sp_check_subset_filter
ms.assetid: 525cfcfc-f317-478d-ba84-72e62285f160
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 29eb4ae1b96c8f9a116b221282ea4b293059b2c4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32989952"
---
# <a name="spchecksubsetfilter-transact-sql"></a>sp_check_subset_filter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用于对任何表检查筛选子句，以确定筛选子句对该表是否有效。 此存储过程返回所提供的筛选器的相关信息，包括筛选器是否适合用于预计算分区。 此存储过程在发布服务器上包含该发布的数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_check_subset_filter [ @filtered_table = ] 'filtered_table'  
        , [ @subset_filterclause = ] 'subset_filterclause'  
    [ , [ @has_dynamic_filters = ] has_dynamic_filters OUTPUT ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@filtered_table**=] *****filtered_table*****  
 筛选的表的名称。 *filtered_table*是**nvarchar(400)**，无默认值。  
  
 [ **@subset_filterclause** =] *****subset_filterclause*****  
 要测试的筛选子句。 *subset_filterclause*是**nvarchar(1000)**，无默认值。  
  
 [ **@has_dynamic_filters**=] *has_dynamic_filters*  
 筛选子句是否是参数化行筛选器。 *has_dynamic_filters*是**位**，默认值为 NULL，是输出参数。 返回的值**1**时筛选器子句是参数化的行筛选器。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|是使用预计算的分区; 如果限定发布其中**1**意味着，可以使用分区，预计算和**0**意味着不能使用。|  
|**has_dynamic_filters**|**bit**|如果提供的筛选器子句包括至少一个参数化的行筛选器;其中**1**表示将使用参数化的行筛选器，和**0**意味着，不使用此类函数。|  
|**dynamic_filters_function_list**|**nvarchar(500)**|筛选子句中动态筛选项目的函数的列表，其中，以分号分隔每个函数。|  
|**uses_host_name**|**bit**|如果[host_name （)](../../t-sql/functions/host-name-transact-sql.md)函数使用在筛选器子句中，其中**1**意味着此函数是存在。|  
|**uses_suser_sname**|**bit**|如果[suser_sname （)](../../t-sql/functions/suser-sname-transact-sql.md)函数使用在筛选器子句中，其中**1**意味着此函数是存在。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_check_subset_filter**合并复制中使用。  
  
 **sp_check_subset_filter**可以执行对任何表中，即使未发布表。 在定义筛选项目之前，此存储过程可以用来验证筛选子句。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_check_subset_filter**。  
  
## <a name="see-also"></a>另请参阅  
 [优化参数化筛选器与预计算分区的性能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)  
  
  
