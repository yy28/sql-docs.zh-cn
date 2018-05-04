---
title: sys.fn_all_changes_&lt;capture_instance&gt; (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- fn_all_changes
- sys.fn_all_changes
- fn_all_changes_TSQL
- sys.fn_all_changes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_all_changes_<capture_instance>
- sys.fn_all_changes_<capture_instance>
ms.assetid: 564fae96-b88c-4f22-9338-26ec168ba6f5
caps.latest.revision: 15
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 733882fa11a2aca2bdcc15f8bb81eb4e4663fd5b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysfnallchangesltcaptureinstancegt-transact-sql"></a>sys.fn_all_changes_&lt;capture_instance&gt; (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包装**所有更改**查询函数。 创建这些函数所必需的脚本由 sys.sp_cdc_generate_wrapper_function 存储过程生成。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
fn_all_changes_<capture_instance> ('start_time' ,'end_time', '<row_filter_option>' )  
  
<capture_instance> ::= The name of the capture instance.  
<row_filter_option> ::=  
{ all  
  | all update old  
}  
```  
  
## <a name="arguments"></a>参数  
 *start_time*  
 **Datetime**值，该值表示要包括在结果集中的更改表项的范围的低端点。  
  
 仅在 cdc。 < capture_instance > _CT 行更改表具有大于关联的提交时间*start_time*包含在结果集。  
  
 如果为此参数提供 NULL 值，则查询范围的低端点对应于捕获实例的有效范围的低端点。  
  
 *end_time*  
 **Datetime**值，该值表示要包括在结果集中的更改表项的范围的高端点。  
  
 此参数可以采用两个可能的含义，具体取决于为选择的值之一上@closed_high_end_point时调用 sys.sp_cdc_generate_wrapper_function 以生成包装器函数的创建脚本：  
  
-   @closed_high_end_point = 1  
  
     只有在 cdc.<capture_instance>_CT 更改表中其关联的提交时间小于或等于 end_time 的行才会包括在结果集中。  
  
-   @closed_high_end_point = 0  
  
     只有在 cdc.capture_instance_CT 更改表中其关联的提交时间严格小于 end_time 的行才会包括在结果集中。  
  
 如果为此参数提供 NULL 值，则查询范围的高端点对应于捕获实例的有效范围的高端点。  
  
 <row_filter_option> ::= { all | all update old }  
 控制结果集中返回的元数据列和行的内容的选项。  
  
 可以是下列选项之一：  
  
 all  
 返回指定 LSN 范围内的所有更改。 对于由于更新操作而导致的更改，此选项仅返回在应用更新后包含新值的行。  
  
 all update old  
 返回指定 LSN 范围内的所有更改。 对于由于更新操作而导致的更改，此选项返回两行，它们分别包含更新前和更新后的列值。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|列类型|Description|  
|-----------------|-----------------|-----------------|  
|__CDC_STARTLSN|**binary(10)**|与更改关联的事务的提交 LSN。 在同一个事务中提交的所有更改都共享同一个提交 LSN。|  
|__CDC_SEQVAL|**binary(10)**|用于对事务中的行更改进行排序的序列值。|  
|\<中的列@column_list>|**各不相同**|在中标识的列*column_list* sp_cdc_generate_wrapper_function 时被调用以生成用于创建包装函数的脚本的自变量。|  
|__CDC_OPERATION|**nvarchar(2)**|操作代码，用于指示将行应用到目标环境时所必需的操作。 它取决于自变量的值*row_filter_option*调用中提供：<br /><br /> *row_filter_option* = 'all'<br /><br /> 'D' - 删除操作<br /><br /> 'I' - 插入操作<br /><br /> 'UN' - 更新操作的新值<br /><br /> *row_filter_option* = all update old<br /><br /> 'D' - 删除操作<br /><br /> 'I' - 插入操作<br /><br /> 'UN' - 更新操作的新值<br /><br /> 'UO' - 更新操作的旧值|  
|\<中的列@update_flag_list>|**bit**|通过将 _uflag 追加到列名称的末尾所命名的位标记。 标志始终设置为 NULL 时\__CDC_OPERATION 具有，I，UO。 当\__CDC_OPERATION 是取消，如果更新生成的相应列的更改设置为 1。 否则为 0。|  
  
## <a name="remarks"></a>注释  
 fn_all_changes_<capture_instance> 函数充当 cdc.fn_cdc_get_all_changes_<capture_instance> 查询函数的包装。 sys.sp_cdc_generate_wrapper 存储过程用于生成用于创建包装的脚本。  
  
 不会自动创建包装函数。 必须做两件事，才能创建包装函数：  
  
1.  运行该存储过程以生成用于创建包装的脚本。  
  
2.  执行该脚本以实际创建包装函数。  
  
 包装器函数使用户能够系统地查询受间隔内发生的更改**datetime** LSN 值通过值而不是。 包装器函数执行之间所提供的所有所需的转换**datetime**值和为查询函数的变量的内部所需的 LSN 值。 当按顺序使用包装函数，来处理更改数据流时，确保没有数据丢失或重复前提是遵循以下约定：@end_time作为提供与一次调用关联间隔的值@start_time与后续调用关联的间隔的值。  
  
 通过在创建脚本时使用 @closed_high_end_point 参数，您可以生成包装以支持指定查询窗口中的闭合上限或开放上限。 就是说，您可以决定其提交时间等于提取间隔的上限的条目是否要包括在间隔中。 默认情况下，包括上限。  
  
 结果集返回**所有更改**包装函数返回 __ $start_lsn 和\_ \_$seqval 列更改表的列作为\__CDC_STARTLSN 和\__CDC_SEQVAL，分别。 它遵循其仅这些中出现的跟踪的列与*@column_list*参数生成包装时间。 如果*@column_list*为 NULL，返回列的所有跟踪源。 源列后跟一个操作列， \__CDC_OPERATION，这是一个标识该操作的一个或两个字符列。  
  
 然后，将位标志追加到在 @update_flag_list 参数中标识的每个列的结果集的末尾。 有关**所有更改**包装，位标志将始终为 NULL，__CDC_OPERATION 是否具有，I 或 UO。 如果\__CDC_OPERATION 是取消，该标志将设置为 1 或 0，具体取决于所更新的操作是否导致对列进行更改。  
  
 变更数据捕获配置模板“实例化架构的 CDC 包装 TVF”显示如何使用 sp_cdc_generate_wrapper_function 存储过程以获取某个架构的已定义查询函数的所有包装函数的 CREATE 脚本。 然后，此模板创建这些脚本。 有关模板的详细信息，请参阅[模板资源管理器](http://msdn.microsoft.com/library/b9ee55c5-bb44-4f76-90ac-792d8d83b4c8)。  
  
## <a name="see-also"></a>另请参阅  
 [sys.sp_cdc_generate_wrapper_function &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
