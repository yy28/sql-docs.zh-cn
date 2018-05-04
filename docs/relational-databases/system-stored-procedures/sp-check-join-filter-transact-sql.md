---
title: sp_check_join_filter (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
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
- filter_TSQL
- sp_check_TSQL
- sp_check_join_filter
- sp_check_join_filter_TSQL
- join
- join_TSQL
- filter
- sp_check
helpviewer_keywords:
- sp_check_join_filter
ms.assetid: e9699d59-c8c9-45f6-a561-f7f95084a540
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6de370018dbfd29078416b9da305a71b98e06680
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spcheckjoinfilter-transact-sql"></a>sp_check_join_filter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用于验证两个表之间的联接筛选器以确定联接筛选子句是否有效。 此存储过程还返回提供的联接筛选器的信息，其中包括联接筛选器是否可用于给定表的预计算分区。 此存储过程在发布服务器的发布中执行。 有关详细信息，请参阅[使用预计算分区优化参数化筛选器性能](../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_check_join_filter [ @filtered_table = ] 'filtered_table'  
        , [@join_table = ] 'join_table'  
        , [ @join_filterclause = ] 'join_filterclause'  
```  
  
## <a name="arguments"></a>参数  
 [ **@filtered_table**=] *****filtered_table*****  
 筛选的表的名称。 *filtered_table*是**nvarchar(400)**，无默认值。  
  
 [ **@join_table**=] *****join_table*****  
 是联接到的表的名称*filtered_table*。 *join_table*是**nvarchar(400)**，无默认值。  
  
 [ **@join_filterclause** =] *****join_filterclause*****  
 要测试的联接筛选子句。 *join_filterclause*是**nvarchar(1000)**，无默认值。  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**can_use_partition_groups**|**bit**|是预计算分区; 如果限定发布其中**1**意味着，可以使用 precomupted 分区，和**0**意味着不能使用。|  
|**has_dynamic_filters**|**bit**|如果提供的筛选器子句包括至少一个参数化筛选函数;其中**1**表示将使用参数化筛选函数，和**0**意味着，不使用此类函数。|  
|**dynamic_filters_function_list**|**nvarchar(500)**|筛选子句中为项目定义参数化筛选器的函数的列表，其中每个函数用分号分隔。|  
|**uses_host_name**|**bit**|如果[host_name （)](../../t-sql/functions/host-name-transact-sql.md)函数使用在筛选器子句中，其中**1**意味着此函数是存在。|  
|**uses_suser_sname**|**bit**|如果[suser_sname （)](../../t-sql/functions/suser-sname-transact-sql.md)函数使用在筛选器子句中，其中**1**意味着此函数是存在。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_check_join_filter**合并复制中使用。  
  
 **sp_check_join_filter**可以执行对任何相关的表中，即使它们未发布。 在定义两个项目之间的联接筛选器之前，可以使用此存储过程验证联接筛选子句。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_check_join_filter**。  
  
## <a name="see-also"></a>另请参阅  
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
