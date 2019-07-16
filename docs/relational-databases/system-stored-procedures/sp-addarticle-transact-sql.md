---
title: sp_addarticle (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addarticle
- sp_addarticle_TSQL
helpviewer_keywords:
- sp_addarticle
ms.assetid: 0483a157-e403-4fdb-b943-23c1b487bef0
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: d56f33a3a5d27ceaf95fe715675f16bd7825cfa9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032947"
---
# <a name="spaddarticle-transact-sql"></a>sp_addarticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建项目并将其添加到发布中。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addarticle [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
    [ , [ @source_table = ] 'source_table' ]  
    [ , [ @destination_table = ] 'destination_table' ]   
    [ , [ @vertical_partition = ] 'vertical_partition' ]   
    [ , [ @type = ] 'type' ]   
    [ , [ @filter = ] 'filter' ]   
    [ , [ @sync_object= ] 'sync_object' ]   
        [ , [ @ins_cmd = ] 'ins_cmd' ]   
    [ , [ @del_cmd = ] 'del_cmd' ]   
        [ , [ @upd_cmd = ] 'upd_cmd' ]   
    [ , [ @creation_script = ] 'creation_script' ]   
    [ , [ @description = ] 'description' ]   
    [ , [ @pre_creation_cmd = ] 'pre_creation_cmd' ]   
    [ , [ @filter_clause = ] 'filter_clause' ]   
    [ , [ @schema_option = ] schema_option ]   
    [ , [ @destination_owner = ] 'destination_owner' ]   
    [ , [ @status = ] status ]   
    [ , [ @source_owner = ] 'source_owner' ]   
    [ , [ @sync_object_owner = ] 'sync_object_owner' ]   
    [ , [ @filter_owner = ] 'filter_owner' ]   
    [ , [ @source_object = ] 'source_object' ]   
    [ , [ @artid = ] article_ID  OUTPUT ]   
    [ , [ @auto_identity_range = ] 'auto_identity_range' ]   
    [ , [ @pub_identity_range = ] pub_identity_range ]   
    [ , [ @identity_range = ] identity_range ]   
    [ , [ @threshold = ] threshold ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @use_default_datatypes = ] use_default_datatypes  
    [ , [ @identityrangemanagementoption = ] identityrangemanagementoption ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @fire_triggers_on_snapshot = ] 'fire_triggers_on_snapshot' ]   
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'` 是包含的项目的名称。 名称在数据库中必须是唯一的。 *发布*是**sysname**，无默认值。  
  
`[ @article = ] 'article'` 是的名称。 该名称在发布中必须唯一。 *文章*是**sysname**，无默认值。  
  
`[ @source_table = ] 'source_table'` 已不推荐使用此参数;使用*source_object*相反。  
  
 *Oracle 发布服务器不支持此参数。*  
  
`[ @destination_table = ] 'destination_table'` 是目标 （订阅） 表的名称，如果不同于*source_table*或存储的过程。 *destination_table*是**sysname**，默认值为 NULL，这意味着， *source_table*等于*destination_table * *。*  
  
`[ @vertical_partition = ] 'vertical_partition'` 启用和禁用对表项目进行筛选的列。 *vertical_partition*是**nchar(5)** ，默认值为 FALSE。  
  
 **false**指示没有垂直筛选并且发布所有列。  
  
 **true**中清除所有除声明的主键列，无默认值为 null 的列和唯一键列。 使用添加列[sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)。  
  
`[ @type = ] 'type'` 是项目的类型。 *类型*是**sysname**，可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**仅限聚合架构**|仅具有架构的聚合函数。|  
|**仅限 func 架构**|仅具有架构的函数。|  
|**索引的视图 logbased**|基于日志的索引视图项目。 Oracle 发布服务器不支持。 对于此类型的项目，不需要单独发布基表。|  
|**索引的视图 logbased manualboth**|具有手动筛选器和手动视图并且基于日志的索引视图项目。 此选项要求同时指定*sync_object*并*筛选器*参数。 对于此类型的项目，不需要单独发布基表。 Oracle 发布服务器不支持。|  
|**索引的视图 logbased manualfilter**|具有手动筛选器并且基于日志的索引视图项目。 此选项要求同时指定*sync_object*并*筛选器*参数。 对于此类型的项目，不需要单独发布基表。 Oracle 发布服务器不支持。|  
|**索引的视图 logbased manualview**|具有手动视图并且基于日志的索引视图项目。 此选项要求您指定*sync_object*参数。 对于此类型的项目，不需要单独发布基表。 Oracle 发布服务器不支持。|  
|**仅限索引的视图架构**|仅具有架构的索引视图。 对于此类型的项目，还必须发布基表。|  
|**logbased** （默认值）|基于日志的项目。|  
|**logbased manualboth**|具有手动筛选器和手动视图并且基于日志的项目。 此选项要求同时指定*sync_object*并*筛选器*参数。 Oracle 发布服务器不支持。|  
|**logbased manualfilter**|具有手动筛选器并且基于日志的项目。 此选项要求同时指定*sync_object*并*筛选器*参数。 Oracle 发布服务器不支持。|  
|**logbased manualview**|具有手动视图并且基于日志的项目。 此选项要求您指定*sync_object*参数。 Oracle 发布服务器不支持。|  
|**proc exec**|将存储过程的执行复制到项目的所有订阅服务器。 Oracle 发布服务器不支持。 我们建议使用选项**serializable proc exec**而不是**proc exec**。 详细信息，请参阅"类型的存储过程执行项目"一节中[事务复制中的发布存储过程执行](../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。 在启用了变更数据捕获的情况下无法使用。|  
|**仅过程架构**|仅具有架构的过程。 Oracle 发布服务器不支持。|  
|**serializable proc exec**|仅当存储过程在可串行事务上下文内执行时才复制存储过程的执行。 Oracle 发布服务器不支持。<br /><br /> 此外必须为要复制的过程执行显式事务内执行过程。|  
|**仅限视图架构**|仅具有架构的视图。 Oracle 发布服务器不支持。 使用此选项时，还必须发布基表。|  
  
`[ @filter = ] 'filter'` 用于水平筛选表的存储的过程 （使用 FOR REPLICATION 创建）。 *筛选器*是**nvarchar(386)** ，默认值为 NULL。 [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)并[sp_articlefilter](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)必须手动执行，以创建视图和筛选存储的过程。 如果不为 NULL，则不创建筛选过程（假定存储过程是手动创建的）。  
  
`[ @sync_object = ] 'sync_object'` 是表或视图用于生成用来表示该项目的快照的数据文件的名称。 *sync_object*是**nvarchar(386)** ，默认值为 NULL。 如果为 NULL， [sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)调用来自动创建用于生成输出文件的视图。 添加包含的任何列后就会出现[sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)。 如果不为 NULL，则不创建视图（假定视图是手动创建的）。  
  
`[ @ins_cmd = ] 'ins_cmd'` 是复制该项目的插入时使用的复制命令类型。 *ins_cmd*是**nvarchar(255)** ，可以是下列值之一。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**NONE**|不执行任何操作。|  
|**CALL sp_MSins_**<br /> **_表_** （默认值）<br /><br /> -或-<br /><br /> **调用 custom_stored_procedure_name**|在订阅服务器中调用要执行的存储过程。 若要使用该复制方法，使用*schema_option*来指定自动创建存储过程，或在项目的每个订阅服务器的目标数据库中创建指定的存储的过程。 *custom_stored_procedure*是用户创建的存储过程的名称。 <strong>sp_MSins_*表*</strong>包含名称的目标表来代替 *（_t)* 参数的一部分。 当*destination_owner*预置到目标表名称的指定。 例如，对于**ProductCategory**表归**生产**订阅服务器上的架构，该参数应为`CALL sp_MSins_ProductionProductCategory`。 在对等复制拓扑中，一篇文章 *（_t)* 追加 GUID 值。 指定*custom_stored_procedure*不支持更新订阅服务器。|  
|**SQL**或为 NULL|复制 INSERT 语句。 需要为 INSERT 语句提供项目中发布的所有列的值。 对插入复制以下命令：<br /><br /> `INSERT INTO <table name> VALUES (c1value, c2value, c3value, ..., cnvalue)`|  
  
 有关详细信息，请参阅[指定如何传播事务项目的更改](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
`[ @del_cmd = ] 'del_cmd'` 是复制该项目的删除时使用的复制命令类型。 *del_cmd*是**nvarchar(255)** ，可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**NONE**|不执行任何操作。|  
|**CALLsp_MSdel_**<br /> **_表_** （默认值）<br /><br /> -或-<br /><br /> **调用 custom_stored_procedure_name**|在订阅服务器中调用要执行的存储过程。 若要使用该复制方法，使用*schema_option*来指定自动创建存储过程，或在项目的每个订阅服务器的目标数据库中创建指定的存储的过程。 *custom_stored_procedure*是用户创建的存储过程的名称。 <strong>sp_MSdel_*表*</strong>包含名称的目标表来代替 *（_t)* 参数的一部分。 当*destination_owner*预置到目标表名称的指定。 例如，对于**ProductCategory**表归**生产**订阅服务器上的架构，该参数应为`CALL sp_MSdel_ProductionProductCategory`。 在对等复制拓扑中，一篇文章 *（_t)* 追加 GUID 值。 指定*custom_stored_procedure*不支持更新订阅服务器。|  
|**XCALL sp_MSdel_**<br /> **_表_**<br /><br /> -或-<br /><br /> **XCALL custom_stored_procedure_name**|采用 XCALL 样式参数调用存储过程。 若要使用该复制方法，使用*schema_option*来指定自动创建存储过程，或在项目的每个订阅服务器的目标数据库中创建指定的存储的过程。 对于更新订阅服务器，不允许指定用户创建的存储过程。|  
|**SQL**或为 NULL|复制 DELETE 语句。 为 DELETE 语句提供所有主键列值。 对删除复制以下命令：<br /><br /> `DELETE FROM <table name> WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
 有关详细信息，请参阅[指定如何传播事务项目的更改](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
`[ @upd_cmd = ] 'upd_cmd'` 是复制该项目的更新时使用的复制命令类型。 *upd_cmd*是**nvarchar(255)** ，可以是下列值之一。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**NONE**|不执行任何操作。|  
|**调用 sp_MSupd_**<br /> **_表_**<br /><br /> -或-<br /><br /> **调用 custom_stored_procedure_name**|在订阅服务器中调用要执行的存储过程。 若要使用该复制方法，使用*schema_option*来指定自动创建存储过程，或在项目的每个订阅服务器的目标数据库中创建指定的存储的过程。|  
|**MCALL sp_MSupd_**<br /> **_表_**<br /><br /> -或-<br /><br /> **MCALL custom_stored_procedure_name**|采用 MCALL 样式参数调用存储过程。 若要使用该复制方法，使用*schema_option*来指定自动创建存储过程，或在项目的每个订阅服务器的目标数据库中创建指定的存储的过程。 *custom_stored_procedure*是用户创建的存储过程的名称。 <strong>sp_MSupd_*表*</strong>包含名称的目标表来代替 *（_t)* 参数的一部分。 当*destination_owner*预置到目标表名称的指定。 例如，对于**ProductCategory**表归**生产**订阅服务器上的架构，该参数应为`MCALL sp_MSupd_ProductionProductCategory`。 在对等复制拓扑中，一篇文章 *（_t)* 追加 GUID 值。 对于更新订阅服务器，不允许指定用户创建的存储过程。|  
|**SCALL sp_MSupd_**<br /> **_表_** （默认值）<br /><br /> -或-<br /><br /> **SCALL custom_stored_procedure_name**|采用 SCALL 样式参数调用存储过程。 若要使用该复制方法，使用*schema_option*来指定自动创建存储过程，或在项目的每个订阅服务器的目标数据库中创建指定的存储的过程。 *custom_stored_procedure*是用户创建的存储过程的名称。 <strong>sp_MSupd_*表*</strong>包含名称的目标表来代替 *（_t)* 参数的一部分。 当*destination_owner*预置到目标表名称的指定。 例如，对于**ProductCategory**表归**生产**订阅服务器上的架构，该参数应为`SCALL sp_MSupd_ProductionProductCategory`。 在对等复制拓扑中，一篇文章 *（_t)* 追加 GUID 值。 对于更新订阅服务器，不允许指定用户创建的存储过程。|  
|**XCALL sp_MSupd_**<br /> **_表_**<br /><br /> -或-<br /><br /> **XCALL custom_stored_procedure_name**|采用 XCALL 样式参数调用存储过程。 若要使用该复制方法，使用*schema_option*来指定自动创建存储过程，或在项目的每个订阅服务器的目标数据库中创建指定的存储的过程。 对于更新订阅服务器，不允许指定用户创建的存储过程。|  
|**SQL**或为 NULL|复制 UPDATE 语句。 UPDATE 语句在所有的列值和主键列值中提供。 对更新复制以下命令：<br /><br /> `UPDATE <table name> SET c1 = c1value, SET c2 = c2value, SET cn = cnvalue WHERE pkc1 = pkc1value AND pkc2 = pkc2value AND pkcn = pkcnvalue`|  
  
> [!NOTE]  
>  对于传播到订阅服务器的数据量，CALL、MCALL、SCALL 和 XCALL 语法各不相同。 CALL 语法传递所有已插入和已删除的列的所有值。 SCALL 语法只传递受影响的列的值。 XCALL 语法传递所有列的值（无论更改与否），包括列以前的值。 有关详细信息，请参阅[指定如何传播事务项目的更改](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)。  
  
`[ @creation_script = ] 'creation_script'` 是的路径和用于在订阅数据库中创建项目的可选项目架构脚本的名称。 *creation_script*是**nvarchar(255)** ，默认值为 NULL。  
  
`[ @description = ] 'description'` 是一文的说明项。 *描述*是**nvarchar(255)** ，默认值为 NULL。  
  
`[ @pre_creation_cmd = ] 'pre_creation_cmd'` 指定系统应执行的操作应用于该项目的快照时检测到订阅服务器上具有相同名称的现有对象时。 *pre_creation_cmd*是**nvarchar(10)** ，可以是下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**无**|不使用命令。|  
|**delete**|在应用快照之前从目标表中删除数据。 水平筛选项目时，将只删除筛选子句所指定的列中的数据。 定义水平筛选时，不支持用于 Oracle 发布服务器。|  
|**删除**（默认值）|删除目标表。|  
|**truncate**|截断目标表。 对 ODBC 或 OLE DB 订阅服务器无效。|  
  
`[ @filter_clause = ] 'filter_clause'` 是的限制 (WHERE) 子句，用于定义水平筛选器。 当输入限制子句时，将省略关键字 WHERE。 *filter_clause*是**ntext**，默认值为 NULL。 有关详细信息，请参阅[筛选已发布数据](../../relational-databases/replication/publish/filter-published-data.md)。  
  
`[ @schema_option = ] schema_option` 为给定项目的架构生成选项的位掩码。 *schema_option*是**binary(8)** ，可以为[|（位或）](../../t-sql/language-elements/bitwise-or-transact-sql.md)产品的一个或多个值：  
  
> [!NOTE]  
>  如果该值为 NULL，则系统将为依赖于其他项目属性的项目自动生成有效的架构选项。 **默认架构选项**给定注释中的表显示了根据项目类型和复制类型的组合将选择的值。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**0x00**|禁用快照代理编写脚本，并使用*creation_script*。|  
|**0x01**|生成对象创建脚本（CREATE TABLE、CREATE PROCEDURE 等）。 该值是存储过程项目的默认值。|  
|**0x02**|如果已定义，则生成传播项目更改的存储过程。|  
|**0x04**|使用 IDENTITY 属性为标识列编写脚本。|  
|**0x08**|复制**时间戳**列。 如果未设置，请**时间戳**列被复制为**二进制**。|  
|**0x10**|生成对应的聚集索引。 即使不设置此选项，但如果已在已发布的表中定义与主键相关的索引以及唯一约束，那么也会生成它们。|  
|**0x20**|在订阅服务器中将用户定义数据类型 (UDT) 转换为基本数据类型。 如果 UDT 列是主键的一部分或者计算列引用 UDT 列，则当 UDT 列上具有 CHECK 或 DEFAULT 约束时，此选项无法使用。 *对 Oracle 发布服务器不支持*。|  
|**0x40**|生成相应的非聚集索引。 即使不设置此选项，但如果已在已发布的表中定义与主键相关的索引以及唯一约束，那么也会生成它们。|  
|**0x80**|复制主键约束。 也会复制与约束相关的任何索引，即使选项**0x10**并**0x40**未启用。|  
|**0x100**|如果已定义，则复制表项目的用户触发器。 *对 Oracle 发布服务器不支持*。|  
|**0x200**|复制外键约束。 如果被所引用的表不是发布的一部分，则不会复制已发布表的任何外键约束。 *对 Oracle 发布服务器不支持*。|  
|**0x400**|复制检查约束。 *对 Oracle 发布服务器不支持*。|  
|**0x800**|复制默认值。 *对 Oracle 发布服务器不支持*。|  
|**0x1000**|复制列级排序规则。<br /><br /> **注意：** Oracle 发布服务器以启用区分大小写的比较，应设置此选项。|  
|**0x2000**|复制与已发布项目源对象关联的扩展属性。 *对 Oracle 发布服务器不支持*。|  
|**0x4000**|复制 UNIQUE 约束。 也会复制与约束相关的任何索引，即使选项**0x10**并**0x40**未启用。|  
|**0x8000**|此选项对 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 发布服务器无效。|  
|**0x10000**|以 NOT FOR REPLICATION 方式复制 CHECK 约束，以便在同步期间不强制执行约束。|  
|**0x20000**|以 NOT FOR REPLICATION 方式复制 FOREIGN KEY 约束，以便在同步期间不强制执行约束。|  
|**0x40000**|复制与已分区表或已分区索引相关联的文件组。|  
|**0x80000**|复制已分区表的分区方案。|  
|**0x100000**|复制已分区索引的分区方案。|  
|**0x200000**|复制表统计信息。|  
|**0x400000**|默认值绑定|  
|**0x800000**|规则绑定|  
|**0x1000000**|全文本索引|  
|**0x2000000**|XML 架构集合绑定到**xml**列不会复制。|  
|**0x4000000**|在复制的索引**xml**列。|  
|**0x8000000**|创建订阅服务器中尚不存在的任何架构。|  
|**0x10000000**|将转换**xml**的列**ntext**在订阅服务器上。|  
|**0x20000000**|将大型对象数据类型 (**nvarchar （max)** ， **varchar （max)** ，并**varbinary （max)** ) 中引入[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]到上受支持的数据类型[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].|  
|**0x40000000**|复制的权限。|  
|**0x80000000**|尝试删除不属于发布一部分的任何对象的依赖项。|  
|**0x100000000**|使用此选项用于复制 FILESTREAM 属性，如果在指定**varbinary （max)** 列。 如果要将表复制到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 订阅服务器，请勿指定此选项。 包含 FILESTREAM 列的表复制[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]不支持订阅服务器，而不考虑如何设置此架构选项。<br /><br /> 请参阅相关的选项**0x800000000**。|  
|**0x200000000**|将日期和时间数据类型转换 (**日期**，**时间**， **datetimeoffset**，以及**datetime2**) 中引入[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]数据在早期版本的支持类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**0x400000000**|复制数据和索引的压缩选项。 有关详细信息，请参阅 [Data Compression](../../relational-databases/data-compression/data-compression.md)。|  
|**0x800000000**|设置此选项可将 FILESTREAM 数据存储到订阅服务器上其自身的文件组中。 如果不设置此选项，FILESTREAM 数据将存储在默认文件组中。 由于复制操作不创建文件组，因此如果您设置此选项，您必须先创建文件组，然后在订阅服务器上应用快照。 有关如何在应用快照之前创建的对象的详细信息，请参阅[执行脚本之前和之后应用快照](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)。<br /><br /> 请参阅相关的选项**0x100000000**。|  
|**0x1000000000**|将公共语言运行时 (CLR) 用户定义类型 (Udt) 大于 8000 字节的转换**varbinary （max)** ，以便类型为 UDT 的列能够复制到订阅服务器正在运行的[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。|  
|**0x2000000000**|将转换**hierarchyid**数据类型设置为**varbinary （max)** ，以便类型的列**hierarchyid**可以复制到订阅服务器正在运行的[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。 有关如何使用详细信息**hierarchyid**列中复制的表，请参阅[hierarchyid &#40;TRANSACT-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)。|  
|**0x4000000000**|复制表的任何筛选的索引。 有关筛选索引的详细信息，请参阅[创建筛选索引](../../relational-databases/indexes/create-filtered-indexes.md)。|  
|**0x8000000000**|将转换**地理**并**geometry**数据类型与**varbinary （max)** ，以使这些类型的列可以复制到订阅服务器运行[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].|  
|**0x10000000000**|复制类型的列的索引**地理**并**geometry**。|  
|**0x20000000000**|复制列的 SPARSE 属性。 有关此属性的详细信息，请参阅[使用稀疏列](../../relational-databases/tables/use-sparse-columns.md)。|  
|**0x40000000000**|启用快照代理在订阅服务器上创建内存优化表编写脚本。|  
|**0x80000000000**|将转换为内存优化项目的非聚集索引的聚集的索引。|  
|**0x400000000000**|复制表的所有非聚集列存储索引|  
|**0x800000000000**|复制表的所有 flitered 非聚集列存储索引。|  
|NULL|复制会自动设置*schema_option*为默认值的值取决于其他项目属性。 “备注”部分的“默认架构选项”表根据项目类型和复制类型列出了默认架构选项。<br /><br /> 默认值为非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布是**0x050D3**。|  
  
 不是所有*schema_option*值对每个复制类型和项目类型是否有效。 **有效架构选项**备注部分中的表显示了可选择的有效架构选项根据项目类型和复制类型的组合。  
  
`[ @destination_owner = ] 'destination_owner'` 是目标对象的名称。 *destination_owner*是**sysname**，默认值为 NULL。 当*destination_owner*未指定，则根据以下规则自动指定所有者：  
  
|条件|目标对象所有者|  
|---------------|------------------------------|  
|发布使用本机模式的大容量复制来生成初始快照，该快照只支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器。|默认值为*source_owner*。|  
|从非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器发布。|默认值为目标数据库的所有者。|  
|发布使用字符模式的大容量复制来生成初始快照，该快照支持非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器。|不分配。|  
  
 若要支持非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器， *destination_owner*必须为 NULL。  
  
`[ @status = ] status` 指定项目是否是用于配置如何传播更改的活动，以及其他选项。 *状态*是**tinyint**，可以为[|（位或）](../../t-sql/language-elements/bitwise-or-transact-sql.md)产品的一个或多个值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|项目是活动的。|  
|**8**|在 INSERT 语句中包含列名。|  
|**16** （默认值）|使用参数化语句。|  
|**24**|在 INSERT 语句中包含列名，并使用参数化语句。|  
|**64**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 例如，使用参数化语句的活动项目在此列中的值为 17。 值为**0**意味着项目处于非活动状态并且未定义任何其他属性。  
  
`[ @source_owner = ] 'source_owner'` 是源对象的所有者。 *source_owner*是**sysname**，默认值为 NULL。 *source_owner*必须为 Oracle 发布服务器指定。  
  
`[ @sync_object_owner = ] 'sync_object_owner'` 是用于定义已发布的项目的所有者。 *sync_object_owner*是**sysname**，默认值为 NULL。  
  
`[ @filter_owner = ] 'filter_owner'` 是筛选器的所有者。 *filter_owner*是**sysname**，默认值为 NULL。  
  
`[ @source_object = ] 'source_object'` 是要发布的数据库对象。 *source_object*是**sysname**，默认值为 NULL。 如果*source_table*为 NULL， *source_object*不能为 NULL。*source_object*应使用而不是*source_table*。 有关可以使用快照复制或事务复制发布的对象的类型的详细信息，请参阅[发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)。  
  
`[ @artid = ] _article_ID_ OUTPUT` 为新项目的项目 ID。 *article_ID*是**int** ，默认值为 NULL，它是一个输出参数。  
  
`[ @auto_identity_range = ] 'auto_identity_range'` 启用和禁用自动标识范围处理在创建的时发布。 *auto_identity_range*是**nvarchar(5)** ，可以是下列值之一：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**true**|启用自动标识范围处理|  
|**false**|禁用自动标识范围处理|  
|NULL（默认值）|通过设置标识范围处理*identityrangemanagementoption*。|  
  
> [!NOTE]  
>  *auto_identity_range*已弃用，并提供用于向后兼容性。 应使用*identityrangemanagementoption*用于指定标识范围管理选项。 有关详细信息，请参阅[复制标识列](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
`[ @pub_identity_range = ] pub_identity_range` 如果将项目的控制发布服务器上的范围大小*identityrangemanagementoption*设置为**自动**或*auto_identity_range*设置为 **，则返回 true**. *pub_identity_range*是**bigint**，默认值为 NULL。 *对 Oracle 发布服务器不支持*。  
  
`[ @identity_range = ] identity_range` 如果将项目的控制订阅服务器上的范围大小*identityrangemanagementoption*设置为**自动**或*auto_identity_range*设置为 **，则返回 true**. *identity_range*是**bigint**，默认值为 NULL。 使用何时*auto_identity_range*设置为**true**。 *对 Oracle 发布服务器不支持*。  
  
`[ @threshold = ] threshold` 是控制分发代理何时分配新标识范围的百分比值。 在指定的值的百分比*阈值*是使用，分发代理将创建一个新的标识范围。 *阈值*是**bigint**，默认值为 NULL。 使用何时*identityrangemanagementoption*设置为**自动**或*auto_identity_range*设置为**true**。 *对 Oracle 发布服务器不支持*。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 确认此存储过程所执行的操作会使现有快照失效。 *force_invalidate_snapshot*是**位**，默认值为 0。  
  
 **0**指定添加项目不会导致快照无效。 如果存储过程检测到更改需要新的快照，则会发生错误并且不进行任何更改。  
  
 **1**指定，将添加一篇文章可能会导致快照无效，并且如果存在订阅，需要新快照，提供了将现有快照标记为过时并生成新快照的权限。  
  
`[ @use_default_datatypes = ] use_default_datatypes` 是发布来自 Oracle 发布服务器项目时是否使用默认列数据类型映射。 *use_default_datatypes*为 bit，默认值为 1。  
  
 **1** = 使用映射的默认项目列。 可以通过执行显示默认数据类型映射[sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)。  
  
 **0** = 自定义项目列定义映射，因此[sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)不由调用**sp_addarticle**。  
  
 当*use_default_datatypes*设置为**0**，则必须执行[sp_changearticlecolumndatatype](../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md)一次针对要更改默认值从每个列映射。 定义所有自定义列映射后，必须执行[sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)。  
  
> [!NOTE]  
>  该参数只应当用于 Oracle 发布服务器。 设置*use_default_datatypes*到**0**为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器将生成错误。  
  
`[ @identityrangemanagementoption = ] identityrangemanagementoption` 指定对项目中如何处理标识范围管理。 *identityrangemanagementoption*是**nvarchar(10)** ，可以是下列值之一。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**无**|复制不会显式执行标识范围管理。 仅当为了保持与 SQL Server 早期版本的向后兼容性时，才建议使用该选项。 禁止用于对等复制。|  
|**手动**|使用 NOT FOR REPLICATION 标记标识列，以启用手动标识范围处理。|  
|**自动**|指定自动管理标识范围。|  
|NULL（默认值）|默认情况下**无**时的值*auto_identity_range*不是**true**。 默认情况下**手动**在对等拓扑默认 (*auto_identity_range*将被忽略)。|  
  
 为了向后兼容时的值*identityrangemanagementoption*为 NULL，则*auto_identity_range*检查。 但是，如果的值*identityrangemanagementoption*为 NULL，则值不是*auto_identity_range*将被忽略。  
  
 有关详细信息，请参阅[复制标识列](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
`[ @publisher = ] 'publisher'` 指定一个非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*添加到项目时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
`[ @fire_triggers_on_snapshot = ] 'fire_triggers_on_snapshot'` 是复制的应用初始快照时执行用户触发器。 *fire_triggers_on_snapshot*是**nvarchar(5)** ，默认值为 FALSE。 **true**意味着应用快照时执行复制的表的用户触发器。 为了使触发器要复制的位掩码值*schema_option*必须包含值**0x100**。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_addarticle**快照复制或事务复制中使用。  
  
 默认情况下，如果复制不支持列数据类型，则复制不发布源表中的任何列。 如果你需要发布这样的列，则必须执行[sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)将列添加。  
  
 将项目添加到支持对等事务复制的发布中时，将应用下列限制：  
  
-   必须为所有基于日志的项目指定参数化语句。 必须包括**16**中*状态*值。  
  
-   目标表的名称和所有者必须与源表匹配。  
  
-   不能水平或垂直筛选项目。  
  
-   不支持自动标识范围管理。 必须指定值为 manual *identityrangemanagementoption*。  
  
-   如果**时间戳**表中存在的列，则必须包括在 0x08 *schema_option*若要复制的列**时间戳**。  
  
-   值为**SQL**不能指定*ins_cmd*， *upd_cmd*，以及*del_cmd*。  
  
 有关详细信息，请参阅 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。  
  
 发布对象时，对象的定义会复制到订阅服务器。 如果要发布的数据库对象依赖于一个或多个其他对象，则必须发布所有被引用对象。 例如，如果要发布的视图依赖于一个表，则也必须发布该表。  
  
 如果*vertical_partition*设置为**true**， **sp_addarticle**交由视图的创建[sp_articleview](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) （之后调用上次[sp_articlecolumn](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)添加)。  
  
 如果发布允许更新订阅，并且已发布的表不具有**uniqueidentifier**列中， **sp_addarticle**添加**uniqueidentifier**列向表自动。  
  
 将复制到不是实例的订阅服务器上时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（异类复制），仅[!INCLUDE[tsql](../../includes/tsql-md.md)]支持语句用于**插入**，**更新**，以及**删除**命令。  
  
 运行日志读取器代理时，将项目添加到对等发布可能导致日志读取器代理和添加该项目的进程之间的死锁。 为了避免此问题，在将项目添加到对等发布前，请使用复制监视器停止正在添加项目的节点上的日志读取器代理。 在添加项目后，重新启动日志读取器代理。  
  
 设置时`@del_cmd = 'NONE'`或`@ins_cmd = 'NONE'`的传播**更新**命令可能还会影响通过不在出现界定的更新时发送这些命令。 （界定更新是来自发布服务器的一种 UPDATE 语句，它复制为订阅服务器上的 DELETE/INSERT 对。）  
  
## <a name="default-schema-options"></a>默认架构选项  
 此表描述了如果设置复制的默认值*schema_options*未指定的用户，其中此值取决于复制类型 （在顶部横向显示） 和项目类型 （第一列纵向显示）。  
  
|项目类型|复制类型||  
|------------------|----------------------|------|  
||事务性|快照|  
|**仅限聚合架构**|**0x01**|**0x01**|  
|**仅限 func 架构**|**0x01**|**0x01**|  
|**仅限索引的视图架构**|**0x01**|**0x01**|  
|**索引的视图 logbased**|**0x30F3**|**0x3071**|  
|**索引的视图底数 manualboth**|**0x30F3**|**0x3071**|  
|**索引的视图 logbased manualfilter**|**0x30F3**|**0x3071**|  
|**索引的视图 logbased manualview**|**0x30F3**|**0x3071**|  
|**logbased**|**0x30F3**|**0x3071**|  
|**logbased manualfilter**|**0x30F3**|**0x3071**|  
|**logbased manualview**|**0x30F3**|**0x3071**|  
|**proc exec**|**0x01**|**0x01**|  
|**仅过程架构**|**0x01**|**0x01**|  
|**serializable proc exec**|**0x01**|**0x01**|  
|**仅限视图架构**|**0x01**|**0x01**|  
  
> [!NOTE]
>  如果发布的排队更新，启用*schema_option*的值**0x80**添加到表中显示的默认值。 默认值*schema_option*对于非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布**0x050D3**。  
  
## <a name="valid-schema-options"></a>有效架构选项  
 此表描述了允许的值*schema_option*基于 （在顶部横向显示） 的复制类型和项目类型 （第一列纵向显示）。  
  
|项目类型|复制类型||  
|------------------|----------------------|------|  
||事务性|快照|  
|**logbased**|所有选项|所有选项，但**0x02**|  
|**logbased manualfilter**|所有选项|所有选项，但**0x02**|  
|**logbased manualview**|所有选项|所有选项，但**0x02**|  
|**索引的视图 logbased**|所有选项|所有选项，但**0x02**|  
|**索引的视图 logbased manualfilter**|所有选项|所有选项，但**0x02**|  
|**索引的视图 logbased manualview**|所有选项|所有选项，但**0x02**|  
|**索引的视图底数 manualboth**|所有选项|所有选项，但**0x02**|  
|**proc exec**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|  
|**serializable proc exec**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|  
|**仅过程架构**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|  
|**仅限视图架构**|**0x01**， **0x010**， **0x020**， **0x040**， **0x0100**， **0x2000**， **而 0x40000 可**， **0x100000**， **0x200000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x40000000**，并**0x80000000**|**0x01**， **0x010**， **0x020**， **0x040**， **0x0100**， **0x2000**， **而 0x40000 可**， **0x100000**， **0x200000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x40000000**，并**0x80000000**|  
|**仅限 func 架构**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|**0x01**， **0x20**， **0x2000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x10000000**， **0x20000000**， **0x40000000**，和**0x80000000**|  
|**仅限索引的视图架构**|**0x01**， **0x010**， **0x020**， **0x040**， **0x0100**， **0x2000**， **而 0x40000 可**， **0x100000**， **0x200000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x40000000**，并**0x80000000**|**0x01**， **0x010**， **0x020**， **0x040**， **0x0100**， **0x2000**， **而 0x40000 可**， **0x100000**， **0x200000**， **0x400000**， **0x800000**， **0x2000000**， **0x8000000**， **0x40000000**，并**0x80000000**|  
  
> [!NOTE]
>  对于排队更新发布*schema_option*的值**0x8000**并**0x80**必须启用。 受支持*schema_option*值为非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]复制时：**0x01**， **0x02**， **0x10**， **0x40**， **0x80**， **0x1000**， **0x4000**并**0X8000**。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-addarticle-transact-sql_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addarticle**。  
  
## <a name="see-also"></a>请参阅  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [sp_articlecolumn (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_articlefilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_articleview &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [复制存储过程 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
