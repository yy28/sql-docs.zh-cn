---
title: "sp_changearticle (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 10/28/2015
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
- sp_changearticle
- sp_changearticle_TSQL
helpviewer_keywords:
- sp_changearticle
ms.assetid: 24c33ca5-f03a-4417-a267-131ca5ba6bb5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3dacb8a0f83084d61c7ca55c5ae093bb57876b82
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="spchangearticle-transact-sql"></a>sp_changearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改事务或快照发布中的项目属性。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_changearticle [ [@publication= ] 'publication' ]  
    [ , [ @article= ] 'article' ]  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication=**] *发布*  
 包含项目的发布的名称。 *发布*是**sysname**，默认值为 NULL。  
  
 [  **@article=**] *文章*  
 将更改其属性的项目的名称。 *文章*是**sysname**，默认值为 NULL。  
  
 [  **@property=**] *属性*  
 要更改的项目属性。 *属性*是**nvarchar(100)**。  
  
 [  **@value=**] *值*  
 项目属性的新值。 *值*是**nvarchar （255)**。  
  
 下表说明项目的属性和这些属性的值。  
  
|“属性”|值|Description|  
|--------------|------------|-----------------|  
|**creation_script**||用于创建目标表的项目架构脚本的路径和名称。 默认值为 NULL。|  
|**del_cmd**||要执行的 DELETE 语句，否则从日志构造。|  
|**description**||项目的新说明项。|  
|**dest_object**||提供该列是为了向后兼容。 使用**dest_table**。|  
|**dest_table**||新目标表。|  
|**destination_owner**||目标对象所有者的名称。|  
|**filter**||要用于筛选表（水平筛选）的新存储过程。 默认值为 NULL。 对于对等复制中的发布，此值不能更改。|  
|**fire_triggers_on_snapshot**|**true**|应用初始快照时会执行已复制的用户触发器。<br /><br /> 注意： 对于触发器要复制的位掩码值*schema_option*必须包括值**0x100**。|  
||**false**|应用初始快照时不会执行已复制的用户触发器。|  
|**identity_range**||控制在订阅服务器中分配的标识范围的大小。 对等复制不支持此属性。|  
|**ins_cmd**||要执行的 INSERT 语句，否则从日志构造。|  
|**pre_creation_cmd**||可以在应用同步之前除去、删除或截断目标表的预创建命令。|  
||**无**|不使用命令。|  
||**拖放**|删除目标表。|  
||**删除**|删除目标表。|  
||**截断**|截断目标表。|  
|**pub_identity_range**||控制在订阅服务器中分配的标识范围的大小。 对等复制不支持此属性。|  
|**schema_option**||为给定项目指定架构生成选项的位图。 *schema_option*是**binary （8)**。 有关详细信息，请参阅本主题后面的备注一节。|  
||**0x00**|通过快照代理禁用脚本。|  
||**0x01**|生成对象创建（CREATE TABLE、CREATE PROCEDURE 等）。|  
||**0x02**|如果已定义，则生成传播项目更改的存储过程。|  
||**0x04，则**|使用 IDENTITY 属性为标识列编写脚本。|  
||**0x08**|复制**时间戳**列。 如果未设置，**时间戳**列被复制为**二进制**。|  
||**0x10**|生成对应的聚集索引。|  
||**0x20**|在订阅服务器中将用户定义数据类型 (UDT) 转换为基本数据类型。 如果 UDT 列是主键的一部分或者计算列引用 UDT 列，则当 UDT 列上具有 CHECK 或 DEFAULT 约束时，此选项无法使用。 Oracle 发布服务器不支持。|  
||**0x40**|生成相应的非聚集索引。|  
||**0x80**|包含已对主键声明的引用完整性。|  
||**0x100**|如果已定义，则复制表项目的用户触发器。|  
||**0x200**|复制 FOREIGN KEY 约束。 如果被引用的表不是发布的一部分，则不会复制已发布表的任何 FOREIGN KEY 约束。|  
||**0x400**|将复制 CHECK 约束。|  
||**0x800**|复制默认值。|  
||**0x1000**|复制列级排序规则。|  
||**0x2000**|复制与已发布项目源对象关联的扩展属性。|  
||**0x4000**|如果在表项目上定义了唯一键，则复制唯一键。|  
||**0x8000**|使用 ALTER TABLE 语句将表项目上的主键和唯一键作为约束复制。<br /><br /> 注意： 此选项已弃用。 使用**0x80**和**0x4000**相反。|  
||**0x10000**|以 NOT FOR REPLICATION 方式复制 CHECK 约束，以便在同步期间不强制执行约束。|  
||**0x20000**|以 NOT FOR REPLICATION 方式复制 FOREIGN KEY 约束，以便在同步期间不强制执行约束。|  
||**而 0x40000 可**|复制与已分区表或已分区索引相关联的文件组。|  
||**0x80000**|复制已分区表的分区方案。|  
||**0x100000**|复制已分区索引的分区方案。|  
||**0x200000**|复制表统计信息。|  
||**0x400000**|默认绑定|  
||**0x800000**|规则绑定|  
||**0x1000000**|全文索引|  
||**0x2000000**|XML 架构集合绑定到**xml**列不会复制。|  
||**0x4000000**|在复制索引**xml**列。|  
||**0x8000000**|创建订阅服务器中尚不存在的任何架构。|  
||**0x10000000**|将转换**xml**列**ntext**订阅服务器上。|  
||**0x20000000**|将大型对象数据类型 (**nvarchar (max)**， **varchar （max)**，和**varbinary （max)**) 中引入[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]到支持的数据类型上[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。|  
||**0x40000000**|复制的权限。|  
||**0x80000000**|尝试删除不属于发布一部分的任何对象的依赖项。|  
||**0x100000000**|使用此选项用于复制 FILESTREAM 属性，如果在指定**varbinary （max)**列。 如果要将表复制到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 订阅服务器，请勿指定此选项。 包含 FILESTREAM 列的表复制[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]不支持订阅服务器，而不考虑如何设置此架构选项。<br /><br /> 请参阅相关的选项**0x800000000**。|  
||**0x200000000**|将日期和时间数据类型转换 (**日期**，**时间**， **datetimeoffset**，和**datetime2**) 中引入[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]在早期版本的支持的数据类型到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
||**0x400000000**|复制数据和索引的压缩选项。 有关详细信息，请参阅 [Data Compression](../../relational-databases/data-compression/data-compression.md)。|  
||**0x800000000**|设置此选项可将 FILESTREAM 数据存储到订阅服务器上其自身的文件组中。 如果不设置此选项，FILESTREAM 数据将存储在默认文件组中。 由于复制操作不创建文件组，因此如果您设置此选项，您必须先创建文件组，然后在订阅服务器上应用快照。 有关如何在应用快照之前创建对象的详细信息，请参阅[将脚本执行之前和之后应用快照](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)。<br /><br /> 请参阅相关的选项**0x100000000**。|  
||**0x1000000000**|将公共语言运行时 (CLR) 用户定义类型 (Udt) 大于 8000 个字节转换**varbinary （max)**以便类型 UDT 的列可以复制到订阅服务器运行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。|  
||**0x2000000000**|将转换**hierarchyid**数据类型设置为**varbinary （max)**以便类型的列**hierarchyid**可以复制到订阅服务器运行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。 有关如何使用**hierarchyid**列中复制的表，请参阅[hierarchyid &#40;Transact SQL &#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
||**0x4000000000**|复制表的任何筛选的索引。 有关筛选的索引的详细信息，请参阅[Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)。|  
||**0x8000000000**|将转换**geography**和**几何图形**数据类型到**varbinary （max)** ，以便这些类型的列可以复制到订阅服务器运行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
||**0x10000000000**|复制类型的列的索引**geography**和**几何图形**。|  
||**0x20000000000**|复制列的 SPARSE 属性。 有关此属性的详细信息，请参阅[使用稀疏列](../../relational-databases/tables/use-sparse-columns.md)。|  
||**0x40000000000**|启用脚本由快照代理在订阅服务器上创建内存优化表。|  
||**0x80000000000**|将转换到的内存优化项目的非聚集索引的聚集的索引。|  
|**status**||指定属性的新状态。|  
||**dts 水平分区**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
||**包含的列名称**|复制的 INSERT 语句中包括列名。|  
||**没有列名称**|复制的 INSERT 语句中不包括列名。|  
||**没有 dts 水平分区**|项目的水平分区不由可转换的订阅定义。|  
||**无**|清除中的所有状态选项[sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md)表并将标记为非活动状态的文章。|  
||**参数**|使用参数化命令将更改传播给订阅服务器。 这是新项目的默认设置。|  
||**字符串文本**|使用字符串文字值将更改传播给订阅服务器。|  
|**sync_object**||用于生成同步输出文件的表或视图的名称。 默认值为 NULL。 Oracle 发布服务器不支持。|  
|**表空间**||标识从 Oracle 数据库发布的项目的日志记录表所使用的表空间。 有关详细信息，请参阅[管理 Oracle 表空间](../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md)。|  
|**阈值**||用于控制分发代理何时分配新标识范围的百分比值。 对等复制不支持此属性。|  
|**类型**||Oracle 发布服务器不支持。|  
||**logbased**|基于日志的项目。|  
||**logbased manualboth**|具有手动筛选器和手动视图并且基于日志的项目。 此选项需要*sync_object*和*筛选器*属性也进行设置。 Oracle 发布服务器不支持。|  
||**logbased manualfilter**|具有手动筛选器并且基于日志的项目。 此选项需要*sync_object*和*筛选器*属性也进行设置。 Oracle 发布服务器不支持。|  
||**logbased manualview**|具有手动视图并且基于日志的项目。 此选项需要*sync_object*属性也设置。 Oracle 发布服务器不支持。|  
||**索引的 viewlogbased**|基于日志的索引视图项目。 Oracle 发布服务器不支持。 对于此类型的项目，不需要单独发布基表。|  
||**索引的 viewlogbased manualboth**|具有手动筛选器和手动视图并且基于日志的索引视图项目。 此选项需要*sync_object*和*筛选器*属性也进行设置。 对于此类型的项目，不需要单独发布基表。 Oracle 发布服务器不支持。|  
||**索引的 viewlogbased manualfilter**|具有手动筛选器并且基于日志的索引视图项目。 此选项需要*sync_object*和*筛选器*属性也进行设置。 对于此类型的项目，不需要单独发布基表。 Oracle 发布服务器不支持。|  
||**索引的 viewlogbased manualview**|具有手动视图并且基于日志的索引视图项目。 此选项需要*sync_object*属性也设置。 对于此类型的项目，不需要单独发布基表。 Oracle 发布服务器不支持。|  
|**upd_cmd**||要执行的 UPDATE 语句，否则从日志构造。|  
|NULL|NULL|返回可更改的项目属性列表。|  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 确认此存储过程所执行的操作是否会使现有快照失效。 *force_invalidate_snapshot*是**位**，默认值为**0**。  
  
 **0**指定文章的更改不会导致快照无效。 如果该存储过程检测到更改确实需要新的快照，则会发生错误，并且不进行任何更改。  
  
 **1**指定文章的更改可能导致快照无效，将需要一次新快照的现有订阅是否可以为现有的快照将被标记为过时和新的快照生成授予的权限。  
  
 有关在更改时需要生成新快照的属性，请参阅“备注”部分。  
  
 [  **@force_reinit_subscription=]***force_reinit_subscription*  
 确认此存储过程执行的操作可能需要重新初始化现有订阅。 *force_reinit_subscription*是**位**默认值为**0**。  
  
 **0**指定文章的更改不会导致要重新初始化的订阅。 如果该存储过程检测到更改将需要重新初始化现有订阅，则会发生错误，并且不进行任何更改。  
  
 **1**指定文章更改导致现有订阅重新初始化订阅，可以授予权限，重新初始化订阅发生。  
  
 有关在更改时需要重新初始化所有现有订阅的属性，请参阅“备注”部分。  
  
 [  **@publisher** =] *发布服务器*  
 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*上更改项目属性时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>Remarks  
 **sp_changearticle**快照复制和事务复制中使用。  
  
 当项目所属的发布，支持对等事务复制时，可以仅更改**说明**， **ins_cmd**， **upd_cmd**，和**del_cmd**属性。  
  
 更改以下属性的任何需要生成新的快照的并且必须指定的值**1**为*force_invalidate_snapshot*参数：  
  
-   **del_cmd**  
  
-   **dest_table**  
  
-   **destination_owner**  
  
-   **ins_cmd**  
  
-   **pre_creation_cmd**  
  
-   **schema_options**  
  
-   **upd_cmd**  
  
 更改以下属性的任何要求该现有订阅重新进行初始化，并且您必须指定的值**1**为*force_reinit_subscription*参数。  
  
-   **del_cmd**  
  
-   **dest_table**  
  
-   **destination_owner**  
  
-   **filter**  
  
-   **ins_cmd**  
  
-   **status**  
  
-   **upd_cmd**  
  
 在现有发布，你可以使用**sp_changearticle**可以更改项目，而无需删除并重新创建整个发布。  
  
> [!NOTE]  
>  更改的值时*schema_option*，系统不执行按位的更新。 这意味着，当你设置*schema_option*使用**sp_changearticle**、 现有位设置可能已关闭。 若要保留现有的设置，你应执行[|（位或）](../../t-sql/language-elements/bitwise-or-transact-sql.md)你设置的值和当前值之间*schema_option*，其可以通过执行确定[sp_helparticle](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)。  
  
## <a name="valid-schema-options"></a>有效架构选项  
 下表描述了允许的值的*schema_option*基于 （横跨顶部显示） 的复制类型和项目类型 （显示的第一列）。  
  
|项目类型|复制类型||  
|------------------|----------------------|------|  
||事务性|快照|  
|**logbased**|所有选项|所有选项但**0x02**|  
|**logbased manualfilter**|所有选项|所有选项但**0x02**|  
|**logbased manualview**|所有选项|所有选项但**0x02**|  
|**索引的视图 logbased**|所有选项|所有选项但**0x02**|  
|**索引的视图 logbased manualfilter**|所有选项|所有选项但**0x02**|  
|**索引的视图 logbased manualview**|所有选项|所有选项但**0x02**|  
|**索引的视图 logbase manualboth**|所有选项|所有选项但**0x02**|  
|**proc exec**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|  
|**可序列化 proc exec**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|  
|**仅限 proc 架构**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|  
|**仅限视图架构**|**0x01**， **0x010**， **0x020**， **0x040**， **0x0100**， **0x2000**， **而 0x40000 可**， **0x100000**， **0x200000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x40000000**，和**0x80000000**|**0x01**， **0x010**， **0x020**， **0x040**， **0x0100**， **0x2000**， **而 0x40000 可**， **0x100000**， **0x200000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x40000000**，和**0x80000000**|  
|**仅限 func 架构**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|  
|**仅限索引的视图架构**|**0x01**， **0x010**， **0x020**， **0x040**， **0x0100**， **0x2000**， **而 0x40000 可**， **0x100000**， **0x200000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x40000000**，和**0x80000000**|**0x01**， **0x010**， **0x020**， **0x040**， **0x0100**， **0x2000**， **而 0x40000 可**， **0x100000**， **0x200000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x40000000**，和**0x80000000**|  
  
> [!NOTE]  
>  对于排队更新发布， *schema_option*值**0x80**必须启用。 支持*schema_option*值非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布是： **0x01**， **0x02**， **0x10**， **0x40**， **0x80**， **0x1000**和**0x4000**。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_changetranarticle](../../relational-databases/replication/codesnippet/tsql/sp-changearticle-transac_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_changearticle**。  
  
## <a name="see-also"></a>另请参阅  
 [查看和修改项目属性](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [更改发布和项目属性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addarticle &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlecolumn (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_droparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)  
  
  
