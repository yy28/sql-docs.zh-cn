---
title: 处理变更数据
ms.custom: seo-dt-2019
ms.date: 01/02/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data [SQL Server]
- change data capture [SQL Server], query function scenarios
- change data capture [SQL Server], LSN boundaries
- change data capture [SQL Server], query functions
ms.assetid: 5346b852-1af8-4080-b278-12efb9b735eb
author: rothja
ms.author: jroth
ms.openlocfilehash: 18002782d7d34b88706b227cf8ac828f9da4976a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889097"
---
# <a name="work-with-change-data-sql-server"></a>处理变更数据 (SQL Server)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]
  可通过表值函数 (TVF) 为变更数据捕获使用者提供更改数据。 这些函数的所有查询均需要使用两个参数来定义日志序列号 (LSN) 范围，在开发返回的结果集时需要考虑这些序列号。 限定这一间隔的较高和较低 LSN 值均包含在间隔中。  
  
 系统提供了几个函数，以帮助确定用于查询 TVF 的相应 LSN 值。 [sys.fn_cdc_get_min_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md) 函数返回与捕获实例有效性间隔关联的最小 LSN。 有效性间隔是指更改数据当前可供其捕获实例使用的时间间隔。 [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) 函数返回有效性间隔中的最大 LSN。 [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) 和 [sys.fn_cdc_map_lsn_to_time](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md) 函数可帮助将 LSN 值置于常规时间线上。 由于变更数据捕获使用闭合查询间隔，因此，有时需要按顺序生成下一个 LSN 值，以确保在连续查询窗口中不会出现重复更改。 [sys.fn_cdc_increment_lsn](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md) 和 [sys.fn_cdc_decrement_lsn](../../relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql.md) 函数在需要对 LSN 值进行增量调整时非常有用。  
  
##  <a name="validating-lsn-boundaries"></a><a name="LSN"></a> 验证 LSN 界限  
 对于要在 TVF 查询中使用的 LSN 界限，我们建议在使用之前对其进行验证。 如果端点为 Null 或位于捕获实例有效性间隔之外，则会强制变更数据捕获 TVF 返回一个错误。  
  
 例如，如果用于定义查询间隔的参数无效，或超出范围，或行筛选器选项无效，则针对所有更改的查询将返回以下错误。  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_all_changes_ ...`  
  
 为 **net changes** 查询返回的相应错误如下所示：  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_net_changes_ ...`  
  
> [!NOTE]  
>  目前已认识到“消息 313”的消息具有误导性，并未提供失败的真正原因。 这种欠妥的用法源于无法从 TVF 中引发显式错误。 然而，即便返回可识别的错误值不准确，也比仅仅返回空结果要好。 无法将空结果集与未返回任何更改的有效查询区分开来。  
  
 如果授权失败，在查询所有更改时将返回失败，如下所示：  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object 'fn_cdc_get_all_changes_...', database 'MyDB', schema 'cdc'.`  
  
 这也适用于净更改查询：  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object fn_cdc_get_net_changes_...', database 'MyDB', schema 'cdc'.`  
  
 有关如何截获这些已知的 TVF 错误并返回有关失败的更有意义的信息的说明，请参阅“使用 TRY CATCH 枚举净更改”模板。  
  
> [!NOTE]  
>  若要在 SQL Server Management Studio 中查找变更数据捕获模板，请在“视图”  菜单上单击“模板资源管理器”  ，展开 **“SQL Server 模板”** ，然后展开 **“变更数据捕获”** 文件夹。  
  
##  <a name="query-functions"></a><a name="Functions"></a> 查询函数  
 根据所跟踪的源表的特性以及配置其捕获实例的方式，将生成一个或两个查询更改数据的 TVF。  
  
-   函数 [cdc.fn_cdc_get_all_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) 返回在指定间隔内发生的所有更改。 将始终生成此函数。 返回的项将始终进行排序：先按更改的事务提交 LSN 进行排序，然后按事务内的更改顺序值进行排序。 根据所选的行筛选器选项，在更新时将返回最终行（行筛选器选项为“all”），或者在更新时返回新值和旧值（行筛选器选项为“all update old”）。  
  
-   当启用源表时，如果将参数 @supports_net_changes 设置为 1，将生成函数 [cdc.fn_cdc_get_net_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)。  
  
    > [!NOTE]  
    >  仅当源表具有定义的主键或已使用 @index_name 参数标识了唯一索引时，才支持此选项。  
  
     **净更改** 函数为每个修改的源表行返回一项更改。 如果在指定间隔内为该行记录了多项更改，列值将反映该行的最终内容。 要确定更新目标环境所需的正确操作，TVF 必须考虑在该间隔内对行执行的初始操作，同时还要考虑对行执行的最终操作。 如果指定了行筛选器选项“all”， **净更改** 查询将返回插入、删除或更新（新值）操作。 此选项始终将更新掩码返回为 Null，这是因为计算聚合掩码会产生开销。 如果需要反映针对某行的所有更改的聚合掩码，请使用“all with mask”选项。 如果下游处理不需要区分插入和更新，请使用“all with merge”选项。 在这种情况下，操作值只采用两个值：1 用于删除，5 用于插入或更新操作。 此选项可避免在确定所派生的操作应该是插入还是更新时所需的附加处理，而且还可在无需区分这些操作时提高查询性能。  
  
 从查询函数中返回的更新掩码是一种简洁表示形式，用于标识某一更改数据行中所有更改的列。 通常，只有捕获列的小型子集需要此信息。 有多个函数可以帮助从掩码中提取信息，以使其更便于应用程序直接使用。 函数 [sys.fn_cdc_get_column_ordinal](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md) 可返回给定捕获实例的命名列的序号位置，而函数 [sys.fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md) 则可以基于函数调用中传递的序号返回所提供的掩码中该位的奇偶性。 在请求更改数据时，可以结合使用这两个函数从掩码中有效地提取并返回信息。 有关如何使用这些函数的说明，请参阅“使用 All With Mask 枚举净更改”模板。  
  
##  <a name="query-function-scenarios"></a><a name="Scenarios"></a> 查询函数应用场景  
 以下部分介绍使用 cdc.fn_cdc_get_all_changes_ < capture_instance > 和 cdc.fn_cdc_get_net_changes_ < capture_instance > 查询函数查询变更数据捕获数据的常用应用场景。  
  
### <a name="querying-for-all-changes-within-the-capture-instance-validity-interval"></a>查询捕获实例有效性间隔中的所有更改  
 请求更改数据的最直接的方式是返回捕获实例的有效性间隔中的所有当前更改数据。 若要发出此请求，请首先确定有效性间隔的 LSN 上限和下限。 然后，使用这些值标识传递到 cdc.fn_cdc_get_all_changes_<capture_instance> 或 cdc.fn_cdc_get_net_changes_<capture_instance> 查询函数的 @from_lsn 和 @to_lsn 参数。 使用 [sys.fn_cdc_get_min_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md) 函数获取下限，使用 [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) 函数获取上限。 有关使用 cdc.fn_cdc_get_all_changes_<capture_instance> 查询函数查询所有当前有效更改的示例代码，请参阅“枚举有效范围中的所有更改”模板。 有关使用 cdc.fn_cdc_get_net_changes_<capture_instance> 函数的类似示例，请参阅“枚举有效范围中的净更改”模板。  
  
### <a name="querying-for-all-new-changes-since-the-last-set-of-changes"></a>查询最近一组更改之后的所有新的更改  
 对于典型应用程序，查询更改数据将是一个不断进行的过程，针对上一次请求之后发生的所有更改发出定期请求。 对于这种查询，可以使用 [sys.fn_cdc_increment_lsn](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md) 函数从上一次查询的上限派生当前查询的下限。 此方法可以确保没有重复的行，这是因为查询间隔始终被视为闭区间，两个端点都包括在间隔中。 然后，使用 [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) 函数获取新的请求间隔的高端点。 有关系统地移动查询时段以获取上一次请求之后的所有更改的示例代码，请参阅“枚举上一次请求之后的所有更改”模板。  
  
### <a name="querying-for-all-new-changes-up-until-now"></a>查询到目前为止的所有新的更改  
 查询函数返回的更改有一个典型约束，即只包括从上一个请求到当前日期和时间发生的更改。 对于此查询，将 sys.fn_cdc_increment_lsn 函数应用到上一次请求中使用的 @from_lsn 值，以确定下限。 由于时间间隔的上限表示为特定时间点，必须先将它转换为 LSN 值，然后查询函数才可以使用它。 在将日期时间值转换为相应的 LSN 值之前，必须确保捕获进程已经处理了指定上限之前提交的所有更改。 为了确保所有符合要求的更改都已经传播到更改表，此操作是必需的。 执行此操作的一种方法是构造一个等待循环，该循环定期进行检查以查看任何数据库更改表的记录的当前最大提交 LSN 是否超出请求间隔所需的结束时间。  
  
 当延迟循环验证捕获进程已经处理了所有相关日志条目之后，请使用 [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) 函数确定以 LSN 值表示的新的高端点。 为了确保检索指定时间之前提交的所有条目，请调用 sys.fn_cdc_map_time_to_lsn 函数，并使用“largest less than or equal”选项。  
  
> [!NOTE]  
>  在不活动期间，会向 cdc.lsn_time_mapping 表添加一个虚条目，以标记捕获进程已经处理了给定提交时间之前的更改的事实。 这样做可以防止使捕获进程看上去已经落后，而实际上只是最近没有任何要处理的更改。  
  
 “枚举到目前为止的所有更改”模板演示如何使用上一个策略查询更改数据。  
  
### <a name="adding-a-commit-time-to-an-all-changes-result-set"></a>向所有更改结果集添加提交时间  
 在 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)表中有每个事务的提交时间，以及数据库更改表中的相关条目。 通过将针对所有更改的请求中返回的 __$start_lsn 值与 cdc.lsn_time_mapping 表条目中的 start_lsn 值相联接，可以返回 tran_end_time 以及更改数据，以将事务在源中的提交时间作为更改的时间戳。 “将提交时间追加到所有更改结果集”模板演示如何执行此联接。  
  
### <a name="joining-change-data-with-other-data-from-the-same-transaction"></a>将更改数据与同一事务的其他数据相联接  
 有时，当在源中提交事务时，将更改数据与收集的有关该事务的其他信息相联接非常有用。 cdc.lsn_time_mapping 表中的 tran_begin_lsn 列提供执行这种联接所需的信息。 当源发生更新时，必须将 [sys.dm_tran_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md) 系统动态视图的 database_transaction_begin_lsn 的值以及要与更改数据相联接的任何其他信息一起保存。 使用 fn_convertnumericlsntobinary 函数比较 database_transaction_begin_lsn 和 tran_begin_lsn 的值。 创建此函数的代码可以在“创建 fn_convertnumericlsntobinary 函数”模板中找到。 “使用给定的 tran_begin_lsn 返回所有更改”模板演示如何使联接生效。  
  
### <a name="querying-using-datetime-wrapper-functions"></a>使用日期时间包装函数进行查询  
 查询更改数据有一个典型应用场景，即使用由日期时间值限定的滑动窗口定期请求更改数据。 对于此类使用者，变更数据捕获提供 [sys.sp_cdc_generate_wrapper_function](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md) 存储过程，该存储过程可生成用于创建变更数据捕获查询函数的自定义包装函数的脚本。 使用这些自定义包装可以将查询间隔表示为日期时间对。  
  
 使用存储过程的调用选项，可以为调用方有权访问的所有捕获实例生成包装，或仅为指定的捕获实例生成包装。 支持的选项还包括能够指定捕获间隔的高端点应为开放还是闭合，结果集中应包括哪些可用的捕获列，以及哪些包含列应具有关联的更新标志。 该过程返回具有两个列的结果集：生成的函数名称（此名称可以从捕获实例名称派生），以及包装存储过程的 Create 语句。 始终生成包装所有更改查询的函数。 如果在创建捕获实例时设置了 @supports_net_changes 参数，还生成包装净更改函数的函数。  
  
 应用程序设计器负责调用脚本生成存储过程，以生成包装存储过程的 Create 语句，并执行生成的创建脚本以创建函数。 当创建捕获实例时，此操作不会自动发生。  
  
 日期时间包装由用户所拥有，不会在调用方的默认架构中创建。 生成的函数适合大多数用户，而不需要修改。 但是，在创建函数之前，始终可以向生成的脚本应用进一步的自定义。  
  
 包装所有更改查询的函数的名称是 fn_all_changes_ 后面跟捕获实例名称。 净更改包装使用的前缀是 fn_net_changes_。 两个函数都有三个参数，正如它们的关联的变更数据捕获 TVF 一样。 但是，包装的查询间隔由两个日期时间值限定，而不是由两个 LSN 值限定。 两组函数的 @row_filter_option 参数相同。  
  
 生成的包装函数支持以下约定，以便系统地遍历变更数据捕获时间线：前一个间隔的 @end_time 参数应用作后一个间隔的 @start_time 参数。 如果遵循此约定，则包装函数负责将日期时间值映射到 LSN 值，并确保不会丢失数据或出现重复数据。  
  
 可以生成包装以支持指定的查询时段上的闭合上限或开放上限。 也就是说，调用方可以指定提交时间等于提取间隔的上限的条目是否要包括在该间隔中。 默认情况下，包括上限。  
  
 如果为 @from_lsn 值或 @to_lsn 值提供了 Null 值，生成的查询 TVF 将失败，而日期时间包装函数则使用 Null 以允许日期时间包装返回所有当前更改。 也就是说，如果将 Null 作为查询时段的低端点传递到日期时间包装，则将在应用到查询 TVF 的基础 SELECT 语句中使用捕获实例有效性间隔的低端点。 同样，如果将 Null 作为查询时段的高端点传递，则当从查询 TVF 进行选择时将使用捕获实例有效性间隔的高端点。  
  
 包装函数返回的结果集包括所有请求的列后面跟一个操作列，该操作列重新编码为一个或两个字符以标识与该行关联的操作。 如果已请求更新标志，则它们将作为位列显示在操作代码之后，并以在 @update_flag_list 参数中指定的顺序显示。 有关自定义生成的日期时间包装的调用选项的信息，请参阅 [sys.sp_cdc_generate_wrapper_function (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)。  
  
 “使用更新标志实例化包装 TVF”模板介绍如何自定义生成的包装函数以将指定列的更新标志追加到净更改查询返回的结果集。 “实例化架构的 CDC 包装 TVF”模板介绍如何将为给定数据库架构中源表创建的所有捕获实例的查询 TVF 的日期时间包装实例化。  
  
 有关使用日期时间包装查询更改数据的示例，请参阅“使用包装和更新标志获取净更改”模板。 此模板演示当包装配置为返回更新标志时，如何使用包装函数查询净更改。 请注意，基础查询函数需要行筛选器选项“all with mask”以在更新时返回非 Null 更新掩码。 为日期时间间隔的上限和下限都传递 Null 值，以便当执行基于 LSN 的基础查询时，指示该函数使用捕获实例的有效性间隔的低端点和高端点。 对于在捕获实例的有效范围内源行发生的每一次修改，查询返回一行。  
  
### <a name="using-the-datetime-wrapper-functions-to-transition-between-capture-instances"></a>使用日期时间包装函数在捕获实例之间转换  
 对于单个被跟踪的源表，变更数据捕获支持最多两个捕获实例。 此功能的主要用途是当源表的数据定义语言 (DDL) 更改扩展了可进行跟踪的列的集合时，在多个捕获实例之间实现转换。 当转换到新的捕获实例时，为了保护较高应用级中基础查询函数的名称不被更改，一个方法是使用包装函数包装基础调用。 然后，确保包装函数的名称保持不变。 当发生切换时，旧包装函数可能会被删除，并创建一个同名的引用新查询函数的新包装函数。 通过首先修改生成的脚本以创建同名的包装函数，可以切换到新捕获实例，而不影响较高应用层。  
  
## <a name="see-also"></a>另请参阅  
 [跟踪数据更改 (SQL Server)](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [关于变更数据捕获 (SQL Server)](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [启用和禁用变更数据捕获 (SQL Server)](../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)   
 [管理和监视变更数据捕获 (SQL Server)](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
