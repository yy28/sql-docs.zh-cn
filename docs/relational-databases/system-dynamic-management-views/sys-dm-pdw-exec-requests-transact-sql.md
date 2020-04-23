---
title: 系统dm_pdw_exec_requests（转用-SQL） |微软文档
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 390225cc-23e8-4051-a5f6-221e33e4c0b4
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 4f4ebcbf84da7d899b4d4cbd861cfb2ae3f75863
ms.sourcegitcommit: c37777216fb8b464e33cd6e2ffbedb6860971b0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82087557"
---
# <a name="sysdm_pdw_exec_requests-transact-sql"></a>系统dm_pdw_exec_requests（转算-SQL）

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存有关 当前或最近处于活动状态[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]的所有请求的信息。 它列出每个请求/查询的一行。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此视图的键。 与请求关联的唯一数字 ID。|系统中所有请求都独一无二。|  
|session_id|**nvarchar(32)**|与运行此查询的会话关联的唯一数字 ID。 请参阅[系统dm_pdw_exec_sessions&#40;交易-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。||  
|status|**nvarchar(32)**|请求的当前状态。|"运行"、"暂停"、"已完成"、"已取消"、"失败"。|  
|submit_time|**datetime**|提交请求以执行的时间。|有效**日期时间**小于或等于当前时间和start_time。|  
|start_time|**datetime**|启动请求执行的时间。|队列请求的 NULL;否则，有效**日期时间**小于或等于当前时间。|  
|end_compile_time|**datetime**|发动机完成编译请求的时间。|尚未编译的请求的 NULL;否则有效**日期时间**小于start_time，小于或等于当前时间。|
|end_time|**datetime**|请求执行完成、失败或取消的时间。|队列或活动请求为空;否则，有效**日期时间**小于或等于当前时间。|  
|total_elapsed_time|**int**|请求启动以来执行时经过的时间（以毫秒为单位）。|介于 0 和start_time和end_time之间的差异之间。</br></br> 如果total_elapsed_time超过整数的最大值，total_elapsed_time将继续为最大值。 此条件将生成警告"已超出最大值"。</br></br> 最大值（以毫秒为单位）与 24.8 天相同。|  
|label|**nvarchar(255)**|与某些 SELECT 查询语句关联的可选标签字符串。|任何包含"a-z"，"A-Z"，"0-9"的字符串。|  
|error_id|**恩瓦尔查尔 （36）**|与请求关联的错误的唯一 ID（如果有）。|请参阅[系统dm_pdw_errors&#40;Transact-SQL&#41;; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md)如果未发生错误，则设置为 NULL。|  
|database_id|**int**|显式上下文（例如，使用 DB_X）使用的数据库标识符。|请参阅系统数据库中的 ID [&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。|  
|command|**nvarchar(4000)**|保存用户提交的请求的全文。|任何有效的查询或请求文本。 超过 4000 字节的查询将被截断。|  
|resource_class|**恩瓦尔查尔 （20）**|用于此请求的工作负载组。 |静态资源类</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>动态资源类</br>小RC</br>中RC</br>大RC</br>XLargeRC|
|importance|**nvarchar(128)**|在"执行"时设置请求的重要性。  这是此工作负荷组和跨工作负荷组中共享资源的请求的相对重要性。  分类器中指定的重要性将覆盖工作负载组重要性设置。</br>适用于：Azure SQL 数据仓库|Null</br>low</br>below_normal</br>正常（默认）</br>above_normal</br>high|
|group_name|**sysname** |对于使用资源的请求，group_name是请求运行下的工作负荷组的名称。  如果请求不利用资源，group_name为空。</br>适用于：Azure SQL 数据仓库|
|classifier_name|**sysname**|对于使用资源的请求，用于分配资源和重要性的分类器的名称。||
|resource_allocation_percentage|**小数（5，2）**|分配给请求的资源的百分比量。</br>适用于：Azure SQL 数据仓库|
|result_cache_hit|**十六进制**|详细说明已完成的查询是否使用了结果集缓存。  </br>适用于：Azure SQL 数据仓库| 1 = 结果集缓存命中 </br> 0 = 结果集缓存未命中 </br> 负值 = 不使用结果集缓存的原因。  有关详细信息，请参阅备注部分。|
||||
  
## <a name="remarks"></a>备注 
 有关此视图保留的最大行的信息，请参阅["容量限制"](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主题中的"元数据"部分。

 result_cache_hit是查询使用结果集缓存的位掩码。  此列可以是[|（从位或）](../../t-sql/language-elements/bitwise-or-transact-sql.md)一个或多个以下值的积：  
  
|值|说明|  
|-----------|-----------------|  
|**1**|结果集缓存命中|  
|-**0 x 00**|结果集缓存错过|  
|-**0x01**|结果集缓存在数据库上禁用。|  
|-**0x02**|结果集缓存在会话上禁用。 | 
|-**0x04**|由于没有查询的数据源，结果集缓存被禁用。|  
|-**0x08**|由于行级安全谓词，结果集缓存被禁用。|  
|-**0 x 10**|由于在查询中使用系统表、临时表或外部表，结果集缓存被禁用。|  
|-**0 x 20**|结果集缓存被禁用，因为查询包含运行时常量、用户定义的函数或非确定性函数。|  
|-**0 x 40**|结果集缓存由于估计的结果集大小为 10GB >而禁用。|  
|-**0 x 80**|结果集缓存被禁用，因为结果集包含大尺寸（>64kb）的行。|  
  
## <a name="permissions"></a>权限

 需要 VIEW SERVER STATE 权限。  
  
## <a name="security"></a>安全性

 sys.dm_pdw_exec_requests 不会根据特定于数据库的权限筛选查询结果。 具有"查看服务器状态"权限的登录可以获取所有数据库的结果查询结果  
  
>[!WARNING]  
>攻击者可以使用 sys.dm_pdw_exec_requests 检索有关特定数据库对象的信息，只需具有"查看服务器状态"权限，并且没有特定于数据库的权限即可检索。  
  
## <a name="see-also"></a>另请参阅

 [SQL 数据仓库和并行数据仓库动态管理视图&#40;处理-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)
