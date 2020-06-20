---
title: 创建函数以检索变更数据 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],creating function
ms.assetid: 55dd0946-bd67-4490-9971-12dfb5b9de94
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 90f754abc2e10732c33c011fdaf8fcd06c0175a4
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84923438"
---
# <a name="create-the-function-to-retrieve-the-change-data"></a>创建函数以检索变更数据
  在完成用于执行变更数据增量加载的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的控制流之后，接下来的任务是创建用于检索变更数据的表值函数。 只需在第一次增量加载之前创建一次此函数。  
  
> [!NOTE]  
>  在创建用于执行变更数据增量加载的包的过程中，第二步是创建用于检索数据的函数。 有关创建此包的总体过程的说明，请参阅[变更数据捕获 (SSIS)](change-data-capture-ssis.md)。  
  
## <a name="design-considerations-for-change-data-capture-functions"></a>变更数据捕获函数的设计注意事项  
 为了检索变更数据，包数据流中的源组件将调用下面的变更数据捕获查询函数之中的一个：  
  
-   **cdc.fn_cdc_get_net_changes_<capture_instance>** 对于此查询，为各更新返回的单个行包含每个变更行的最终状态。 在大多数情况下，您只需要净更改查询返回的数据。 有关详细信息，请参阅[cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; (Transact-SQL)](/sql/relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql)。  
  
-   **cdc.fn_cdc_get_all_changes_<capture_instance>** 此查询返回捕获间隔期间各行中发生的所有更改。 有关详细信息，请参阅 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  (Transact-SQL)](/sql/relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql)。  
  
 然后，源组件获取函数返回的结果并将这些结果传递到下游转换和目标，以将变更数据应用到最终目标。  
  
 但是， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 源组件无法直接调用这些变更数据捕获函数。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 源组件需要有关查询所返回列的元数据。 变更数据捕获函数不定义其输出表的列。 因此，这些函数不会为 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 源组件返回足够的元数据。  
  
 相反，因为表值包装函数在其 RETURNS 子句中显式定义了其输出表的列，所以应使用该函数。 列的显式定义提供了 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 源组件所需的元数据。 必须为每个要检索变更数据的表创建此函数。  
  
 有两种方法可创建调用变更数据捕获查询函数的表值包装函数：  
  
-   可以调用 **sys.sp_cdc_generate_wrapper_function** 系统存储过程来创建表值函数。  
  
-   可以使用本主题中的准则和示例编写自己的表值函数。  
  
## <a name="calling-a-stored-procedure-to-create-the-table-valued-function"></a>调用存储过程来创建表值函数  
 创建所需表值函数最快速且简便的方法是调用 **sys.sp_cdc_generate_wrapper_function** 系统存储过程。 此存储过程生成用于创建包装函数的脚本，这些脚本是专为满足 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 源组件的需要而设计的。  
  
> [!IMPORTANT]  
>  **sys.sp_cdc_generate_wrapper_function** 系统存储过程不直接创建包装函数。 存储过程为包装函数生成 CREATE 脚本。 开发人员必须运行存储过程生成的 CREATE 脚本，然后增量加载包才能调用包装函数。  
  
 若要了解如何使用此系统存储过程，您应该了解该过程的执行内容、该过程生成的脚本以及这些脚本创建的包装函数。  
  
### <a name="understanding-and-using-the-stored-procedure"></a>了解和使用存储过程  
 **sys.sp_cdc_generate_wrapper_function** 系统存储过程生成脚本，这些脚本用于创建供 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包使用的包装函数。  
  
 下面是存储过程定义的前几行：  
  
 `CREATE PROCEDURE sys.sp_cdc_generate_wrapper_function`  
  
 `(`  
  
 `@capture_instance sysname = null`  
  
 `@closed_high_end_point bit = 1,`  
  
 `@column_list = null,`  
  
 `@update_flag_list = null`  
  
 `)`  
  
 该存储过程的所有参数都是可选的。 如果您在调用该存储过程时不提供任何参数的值，存储过程将为您具有访问权限的所有捕获实例创建包装函数。  
  
> [!NOTE]  
>  有关此存储过程的语法及其参数的详细信息，请参阅 [sys.sp_cdc_generate_wrapper_function (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql)。  
  
 该存储过程会始终生成从每个捕获实例返回所有变更的包装函数。 如果在 *@supports_net_changes* 创建捕获实例时设置了参数，则该存储过程还会生成一个包装函数，以从每个适用的捕获实例返回净更改。  
  
 该存储过程返回带有两列的结果集：  
  
-   该存储过程生成的包装函数的名称。 此存储过程从捕获实例的名称派生函数名称。 （函数名称是“fn_all_changes_”后跟捕获实例名。 如果创建的是净变更函数，则其前缀为“fn_net_changes_”。）  
  
-   包装函数的 CREATE 语句。  
  
### <a name="understanding-and-using-the-scripts-created-by-the-stored-procedure"></a>了解和使用存储过程创建的脚本  
 通常，开发人员使用 INSERT...EXEC 语句调用 **sys.sp_cdc_generate_wrapper_function** 存储过程，并将该存储过程创建的脚本保存到临时表中。 然后，可以单独选择每个脚本，并运行该脚本以创建相应的包装函数。 但是，开发人员还可以使用一组 SQL 命令运行所有的 CREATE 脚本，如以下示例代码中所示：  
  
```  
create table #wrapper_functions  
      (function_name sysname, create_stmt nvarchar(max))  
insert into #wrapper_functions  
exec sys.sp_cdc_generate_wrapper_function  
  
declare @stmt nvarchar(max)  
declare #hfunctions cursor local fast_forward for   
      select create_stmt from #wrapper_functions  
open #hfunctions  
fetch #hfunctions into @stmt  
while (@@fetch_status <> -1)  
begin  
      exec sp_executesql @stmt  
      fetch #hfunctions into @stmt  
end  
close #hfunctions  
deallocate #hfunctions  
```  
  
### <a name="understanding-and-using-the-functions-created-by-the-stored-procedure"></a>了解和使用存储过程创建的函数  
 为了系统地遍历捕获的变更数据的时间线，生成的包装函数需要 *@end_time* 一个间隔的参数作为 *@start_time* 后续间隔的参数。 遵循此约定时，生成的包装函数可执行以下任务：  
  
-   将日期/时间值映射为内部使用的 LSN 值。  
  
-   确保没有数据丢失或重复。  
  
 为了简化对更改表的所有行的查询，生成的包装函数还支持以下约定：  
  
-   如果 @start_time 参数为 Null，包装函数使用捕获实例中最低的 LSN 值作为查询的下限。  
  
-   如果 @end_time 参数为 Null，包装函数使用捕获实例中最高的 LSN 值作为查询的上限。  
  
 大部分用户应该能够使用 **sys.sp_cdc_generate_wrapper_function** 系统存储过程创建的包装函数而无需进行修改。 但是，若要自定义包装函数，您必须自定义 CREATE 脚本，然后再运行该脚本。  
  
 当您的包调用包装函数时，该包必须为三个参数提供值。 这三个参数类似于变更数据捕获函数使用的三个参数。 这三个参数分别是：  
  
-   时间间隔的起始日期/时间值和结束日期/时间值。 包装函数使用日期/时间值作为查询间隔的端点，而变更数据捕获函数使用两个 LSN 值作为端点。  
  
-   行筛选器。 对于包装函数和变更数据捕获函数， *@row_filter_option* 参数是相同的。 有关详细信息，请参阅 [cdc.fn_cdc_get_all_changes_<capture_instance> (Transact-SQL)](/sql/relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql) 和 [cdc.fn_cdc_get_net_changes_<capture_instance> (Transact SQL)](/sql/relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql)。  
  
 包装函数返回的结果集包含以下数据：  
  
-   请求的所有变更数据列。  
  
-   名为 __CDC_OPERATION 的列，该列使用单字符或双字符字段来标识与该行关联的操作。 此字段的有效值如下：“I”表示插入，“D”表示删除，“UO”表示更新旧值，“UN”表示更新新值。  
  
-   在请求标记时更新标志，这些标志在操作代码和参数中指定的顺序中显示为位列 *@update_flag_list* 。 这些列的命名方式是在关联的列名后追加“_uflag”。  
  
 如果你的包调用查询所有变更的包装函数，该包装函数还将返回列 __CDC_STARTLSN 和 \__CDC_SEQVAL。 这两列分别成为结果集的第一列和第二列。 包装函数还将基于这两列对结果集进行排序。  
  
## <a name="writing-your-own-table-value-function"></a>编写自己的表值函数  
 还可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 编写自己的可调用变更数据捕获查询函数的表值包装函数，并将该表值包装函数存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中。 有关如何创建 Transact-SQL 函数的详细信息，请参阅 [CREATE FUNCTION (Transact-SQL)](/sql/t-sql/statements/create-function-transact-sql)。  
  
 下面的示例定义一个表值函数，该表值函数将检索 Customer 表在指定的变更间隔发生的变更。 此函数使用变更数据捕获函数将 `datetime` 值映射到变更表内部使用的二进制日志序列号 (LSN) 值。 此函数还可以处理以下几种特殊情况：  
  
-   将 null 值传递到开始时间时，函数将采用最早的可用值。  
  
-   将 null 值传递到结束时间时，函数将采用最晚的可用值。  
  
-   如果开始的 LSN 与结束的 LSN 相等，则通常指示所选间隔不存在记录，此函数会退出。  
  
### <a name="example-of-a-table-value-function-that-queries-for-change-data"></a>查询变更数据的表值函数示例  
  
```  
CREATE function CDCSample.uf_Customer (  
     @start_time datetime  
    ,@end_time datetime  
)  
returns @Customer table (  
     CustomerID int  
    ,TerritoryID int  
    ,CustomerType nchar(1)  
    ,rowguid uniqueidentifier  
    ,ModifiedDate datetime  
    ,CDC_OPERATION varchar(1)  
) as  
begin  
    declare @from_lsn binary(10), @to_lsn binary(10)  
  
    if (@start_time is null)  
        select @from_lsn = sys.fn_cdc_get_min_lsn('Customer')  
    else  
        select @from_lsn = sys.fn_cdc_increment_lsn(sys.fn_cdc_map_time_to_lsn('largest less than or equal',@start_time))  
  
    if (@end_time is null)  
        select @to_lsn = sys.fn_cdc_get_max_lsn()  
    else  
        select @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal',@end_time)  
  
    if (@from_lsn = sys.fn_cdc_increment_lsn(@to_lsn))  
        return  
  
    -- Query for change data  
    insert into @Customer  
    select   
        CustomerID,      
        TerritoryID,   
        CustomerType,   
        rowguid,   
        ModifiedDate,   
        case __$operation  
                when 1 then 'D'  
                when 2 then 'I'  
                when 4 then 'U'  
                else null  
         end as CDC_OPERATION  
    from   
        cdc.fn_cdc_get_net_changes_Customer(@from_lsn, @to_lsn, 'all')  
  
    return  
end   
go  
  
```  
  
### <a name="retrieving-additional-metadata-with-the-change-data"></a>检索带有变更数据的其他元数据  
 尽管上述用户创建的表值函数仅使用 **__$operation** 列，**cdc.fn_cdc_get_net_changes_<capture_instance>** 函数将针对每个变更行返回四列元数据。 如果想要在数据流中使用这些值，可以从表值包装函数中将它们作为额外的列返回。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|`binary(10)`|与更改的提交事务关联的 LSN。<br /><br /> 在同一事务中提交的所有更改将共享同一个提交 LSN。 例如，如果对源表的更新操作修改了两个不同的行，则更改表将包含四行（两行具有旧值，两行具有新值），每一行均具有相同的 **__$start_lsn** 值。|  
|**__$seqval**|`binary(10)`|用于对事务中的行更改进行排序的序列值。|  
|**__ $ 操作**|`int`|与更改关联的数据操作语言 (DML) 操作。 可以是以下值之一：<br /><br /> 1 = 删除<br /><br /> 2 = 插入<br /><br /> 3 = 更新（执行更新操作前的值。）<br /><br /> 4 = 更新（执行更新操作后的值。）|  
|**__ $ update_mask**|`varbinary(128)`|基于变更表的列序号的位掩码，用于标识那些发生了变更的列。 如果需要确定哪些列发生了更改，则可检查此值。|  
|**\<captured source table columns>**|多种多样|函数返回的其余列是在创建捕获实例时源表中标识为已捕获列的那些列。 如果已捕获列的列表中最初未指定任何列，则将返回源表中的所有列。|  
  
 有关详细信息，请参阅[cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; (Transact-SQL)](/sql/relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql)。  
  
## <a name="next-step"></a>后续步骤  
 在创建了用于查询变更数据的表值函数之后，下一步就是开始设计包中的数据流。  
  
 **下一个主题：** [检索和了解变更数据](retrieve-and-understand-the-change-data.md)  
  
  
