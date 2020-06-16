---
title: sys. dm_pdw_exec_requests （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: 982096893cdce9c4b604df9c3fb0258cefaaf93d
ms.sourcegitcommit: 7d6eb09588ff3477cf39a8fd507d537a603bc60d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2020
ms.locfileid: "84796518"
---
# <a name="sysdm_pdw_exec_requests-transact-sql"></a>sys. dm_pdw_exec_requests （Transact-sql）

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  保存有关中当前或最近活动的所有请求的信息 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。 每个请求/查询在表中各占一行。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|此视图的键。 与请求关联的唯一数字 ID。|系统中所有请求都是唯一的。|  
|session_id|**nvarchar(32)**|与运行此查询的会话相关联的唯一数字 ID。 请参阅[sys.databases &#40;transact-sql&#41;dm_pdw_exec_sessions ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。||  
|状态|**nvarchar(32)**|请求的当前状态。|"正在运行"、"已挂起"、"已完成"、"已取消"、"已失败"。|  
|submit_time|**datetime**|提交请求以执行的时间。|有效的**日期**时间小于或等于当前时间，start_time。|  
|start_time|**datetime**|开始执行请求的时间。|对于排队的请求为 NULL;否则，有效的**日期时间**小于或等于当前时间。|  
|end_compile_time|**datetime**|引擎完成编译请求的时间。|对于尚未编译的请求，为 NULL;否则，有效的**日期时间**小于 start_time 且小于或等于当前时间。|
|end_time|**datetime**|请求执行完成、失败或已取消的时间。|对于排队或活动的请求为 Null;否则，有效的**日期**时间小于或等于当前时间。|  
|total_elapsed_time|**int**|自请求开始后执行所用的时间（以毫秒为单位）。|介于0与 start_time 与 end_time 之间的差异。</br></br> 如果 total_elapsed_time 超过整数的最大值，则 total_elapsed_time 将继续作为最大值。 此条件将生成警告 "已超过最大值。"</br></br> 最大值（以毫秒为单位）与24.8 天相同。|  
|标签|**nvarchar(255)**|与某些 SELECT 查询语句相关联的可选标签字符串。|包含 "a-z"、"a-z"、"0-9" 和 "_" 的任何字符串。|  
|error_id|**nvarchar （36）**|与请求关联的错误的唯一 ID （如果有）。|请参阅[dm_pdw_errors &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-errors-transact-sql.md);如果未发生错误，则设置为 NULL。|  
|database_id|**int**|显式上下文使用的数据库的标识符（例如，使用 DB_X）。|请参阅 sys.databases 中的 ID [&#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。|  
|命令|**nvarchar(4000)**|保存用户提交的请求的完整文本。|任何有效的查询或请求文本。 超过4000字节的查询将被截断。|  
|resource_class|**nvarchar （20）**|用于此请求的工作负荷组。 |静态资源类</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80</br>            </br>动态资源类</br>SmallRC</br>MediumRC</br>LargeRC</br>XLargeRC|
|importance|**nvarchar(128)**|执行请求的重要性设置。  这是此工作负荷组中的请求与共享资源的工作负荷组之间的相对重要性。  分类器中指定的重要性覆盖工作负荷组重要性设置。</br>适用于：Azure SQL 数据仓库|Null</br>low</br>below_normal</br>normal （默认值）</br>above_normal</br>high|
|group_name|**sysname** |对于利用资源的请求，group_name 是在其下运行请求的工作负荷组的名称。  如果请求不使用资源，则 group_name 为 null。</br>适用于：Azure SQL 数据仓库|
|classifier_name|**sysname**|对于利用资源的请求，是用于分配资源和重要性的分类器的名称。||
|resource_allocation_percentage|**decimal （5，2）**|分配给请求的资源的百分比。</br>适用于：Azure SQL 数据仓库|
|result_cache_hit|**decimal**|详细说明已完成的查询是否使用了结果集缓存。  </br>适用于：Azure SQL 数据仓库| 1 = 结果集缓存命中 </br> 0 = 结果集缓存未命中 </br> 负值 = 未使用结果集缓存的原因。  有关详细信息，请参阅备注部分。|
||||
  
## <a name="remarks"></a>备注 
 有关此视图保留的最大行的信息，请参阅[容量限制](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata)主题中的元数据部分。

 Result_cache_hit 是查询对结果集缓存的使用的位掩码。  此列可以是[|（位或）](../../t-sql/language-elements/bitwise-or-transact-sql.md)以下一个或多个值的产品：  
  
|值|说明|  
|-----------|-----------------|  
|**1**|结果集缓存命中|  
|-**0x00**|结果集缓存未命中|  
|-**0x01**|已对数据库禁用结果集缓存。|  
|-**0x02**|在会话上禁用结果集缓存。 | 
|-**0x04**|由于没有用于查询的数据源，因此已禁用结果集缓存。|  
|-**0x08**|由于行级安全谓词，结果集缓存已禁用。|  
|-**0x10**|由于在查询中使用了系统表、临时表或外部表，因此结果集缓存已禁用。|  
|-**0x20**|由于查询包含运行时常量、用户定义函数或非确定性函数，因此禁用了结果集缓存。|  
|-**0x40**|由于估计的结果集大小为 >10GB，结果集缓存已禁用。|  
|-**0x80**|结果集缓存已禁用，因为结果集包含大小较大（>64kb）的行。|  
  
## <a name="permissions"></a>权限

 需要 VIEW SERVER STATE 权限。  
  
## <a name="security"></a>安全性

 sys. dm_pdw_exec_requests 不根据特定于数据库的权限来筛选查询结果。 具有 VIEW SERVER STATE 权限的登录名可以获取所有数据库的结果查询结果  
  
>[!WARNING]  
>攻击者可以使用 dm_pdw_exec_requests sys.databases 来检索有关特定数据库对象的信息，只需具有 VIEW SERVER STATE 权限，而无需具有数据库特定的权限即可。  
  
## <a name="see-also"></a>另请参阅

 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)
