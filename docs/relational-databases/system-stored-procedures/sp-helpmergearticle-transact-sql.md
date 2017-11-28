---
title: "sp_helpmergearticle (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_helpmergearticle
- sp_helpmergearticle_TSQL
helpviewer_keywords: sp_helpmergearticle
ms.assetid: 0fb9986a-3c33-46ef-87bb-297396ea5a6a
caps.latest.revision: "40"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 970c07111ba123be3262f9effb5c87a26bb14960
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpmergearticle-transact-sql"></a>sp_helpmergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关项目的信息。 此存储过程用于在发布服务器上对发布数据库执行，或在正重新发布的订阅服务器上对订阅数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpmergearticle [ [ @publication = ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication=**] *发布*  
 要检索其相关信息的发布的名称。 *发布*是**sysname**，默认值为 **%** ，这将返回有关当前数据库中的所有发布中包含的所有合并项目的信息。  
  
 [  **@article=**] *文章*  
 要返回其信息的项目的名称。 *文章*是**sysname**，默认值为 **%** ，它在给定的发布中返回有关所有合并项目的信息。  
  
## <a name="result-set"></a>结果集  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|项目标识符。|  
|**名称**|**sysname**|项目的名称。|  
|**source_owner**|**sysname**|源对象所有者的名称。|  
|**source_object**|**sysname**|从其中添加项目的源对象的名称。|  
|**sync_object_owner**|**sysname**|定义发布项目的视图所有者的名称。|  
|**sync_object**|**sysname**|用于建立分区初始数据的自定义对象的名称。|  
|**说明**|**nvarchar(255)**|对项目的说明。|  
|**status**|**tinyint**|项目的状态，可以为以下值之一：<br /><br /> **1** = 处于非活动状态<br /><br /> **2** = 活动<br /><br /> **5** = 挂起的数据定义语言 (DDL) 操作<br /><br /> **6** = 使用新生成快照的 DDL 操作<br /><br /> 注意： 当项目重新初始化订阅时，值的**5**和**6**更改为**2**。|  
|**creation_script**|**nvarchar(255)**|用于在订阅数据库中创建项目的可选项目架构脚本的路径和名称。|  
|**conflict_table**|**nvarchar(270)**|存储插入或更新冲突的表的名称。|  
|**article_resolver**|**nvarchar(255)**|项目的自定义冲突解决程序。|  
|**subset_filterclause**|**nvarchar(1000)**|用于指定水平筛选的 WHERE 子句。|  
|**pre_creation_command**|**tinyint**|预创建方法，可以为以下值之一：<br /><br /> **0** = none<br /><br /> **1** = drop<br /><br /> **2** = delete<br /><br /> **3** = 截断|  
|**schema_option**|**binary （8)**|项目的架构生成选项位图。 有关此位图选项的信息，请参阅[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)或[sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)。|  
|**type**|**int**|项目类型，可以为以下值之一：<br /><br /> **10** = 表<br /><br /> **32** = 存储的过程<br /><br /> **64** = 视图或索引视图<br /><br /> **128** = 用户定义函数<br /><br /> **160** = 仅限同义词架构|  
|**column_tracking**|**int**|设置列级跟踪;其中**1**意味着列级跟踪处于启用状态，和**0**意味着列级跟踪处于关闭状态。|  
|**resolver_info**|**nvarchar(255)**|项目冲突解决程序名。|  
|**vertical_partition**|**bit**|如果垂直分区文章;其中**1**意味着，垂直分区文章，和**0**意味着，它不是。|  
|**destination_owner**|**sysname**|目标对象的所有者。 只适用于合并存储过程、视图和用户定义函数 (UDF) 架构项目。|  
|**identity_support**|**int**|如果已启用自动标识范围处理;其中**1**启用和**0**处于禁用状态。|  
|**pub_identity_range**|**bigint**|分配新标识值时要使用的范围大小。 有关详细信息，请参阅的"合并复制"部分[复制标识列](../../relational-databases/replication/publish/replicate-identity-columns.md)。|  
|**identity_range**|**bigint**|分配新标识值时要使用的范围大小。 有关详细信息，请参阅的"合并复制"部分[复制标识列](../../relational-databases/replication/publish/replicate-identity-columns.md)。|  
|**阈值**|**int**|用于运行的订阅服务器的百分比值[!INCLUDE[ssEW](../../includes/ssew-md.md)]或以前版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 **阈值**控制何时合并代理指派的新标识范围。 如果使用了在阈值中指定的百分比值，合并代理将创建新的标识范围。 有关详细信息，请参阅的"合并复制"部分[复制标识列](../../relational-databases/replication/publish/replicate-identity-columns.md)。|  
|**verify_resolver_signature**|**int**|如果在使用合并复制; 中的解析程序前验证数字签名其中**0**意味着，不验证签名，和**1**意味着验证的签名以查看它是否来自可靠来源。|  
|**destination_object**|**sysname**|目标对象的名称。 只适用于合并存储过程、视图和 UDF 架构项目。|  
|**allow_interactive_resolver**|**int**|如果在一篇文章; 上使用交互式冲突解决程序其中**1**表示将使用此解析程序，和**0**意味着未使用。|  
|**fast_multicol_updateproc**|**int**|启用或禁用合并代理以将更改应用到一个 UPDATE 语句; 中同一行中的多个列其中**1**意味着多个列都在一个语句中，更新和**0**单独的 UPDATE 语句的方法是为每个更新的列的问题。|  
|**check_permissions**|**int**|一个整数值，表示已验证的表级权限的位图。 有关可能的值的列表，请参阅[sp_addmergearticle &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**processing_order**|**int**|数据更改应用于发布中的项目的顺序。|  
|**upload_options**|**tinyint**|定义对具有客户端订阅的订阅服务器上所进行更新的限制，可以为下列值之一：<br /><br /> **0** = 没有在客户端订阅与订阅服务器上所做的更新限制; 所有的更改上载到发布服务器。<br /><br /> **1** = 对于客户端订阅，订阅服务器上允许更改但不是会上载到发布服务器。<br /><br /> **2** = 在订阅服务器与客户端订阅不允许更改。<br /><br /> 有关详细信息，请参阅[使用仅下载项目优化合并复制性能](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)。|  
|**identityrangemanagementoption**|**int**|如果已启用自动标识范围处理;其中**1**启用和**0**处于禁用状态。|  
|**delete_tracking**|**bit**|如果删除被复制;其中**1**意味着，删除复制，和**0**意味着，它们不是。|  
|**是 compensate_for_errors**|**bit**|指示是否在同步; 期间遇到错误时采取补偿操作其中**1**指示，都将使用补偿操作，和**0**意味着不会采取补偿操作。|  
|**partition_options**|**tinyint**|定义项目数据的分区方式，当所有行只属于一个分区或只属于一个订阅时，这将可以实现性能优化。 *partition_options*可以是以下值之一。<br /><br /> **0** = 筛选的项目是静态的或不会生成每个分区的数据的唯一子集; 即，它是"重叠"分区。<br /><br /> **1** = 分区重叠，并且订阅服务器上的数据操作语言 (DML) 更新不能更改行属于哪个分区。<br /><br /> **2** = 筛选文章生成不重叠分区，但多个订阅服务器可以接收相同的分区。<br /><br /> **3** = 筛选的项目生成对每个订阅都是唯一的不重叠分区。|  
|**artid**|**uniqueidentifier**|唯一标识项目的标识符。|  
|**pubid**|**uniqueidentifier**|唯一标识在其中发布项目的发布的标识符。|  
|**stream_blob_columns**|**bit**|表示在复制二进制大型对象列时是否使用数据流优化。 **1**意味着，正在使用优化，和**0**意味着不使用优化。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_helpmergearticle**合并复制中使用。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**db_owner**在发布数据库中，固定数据库角色**replmonitor**分发数据库中或为发布的发布访问列表中的角色可以执行**sp_helpmergearticle**。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_helpmergearticle](../../relational-databases/replication/codesnippet/tsql/sp-helpmergearticle-tran_1.sql)]  
  
## <a name="see-also"></a>另请参阅  
 [查看和修改项目属性](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [sp_addmergearticle &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_dropmergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
