---
title: "sys.fn_net_changes_&lt;capture_instance&gt; (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server (starting with 2008)
f1_keywords:
- sys.fn_net_changes_TSQL
- fn_net_changes_TSQL
- fn_net_changes
- sys.fn_net_changes
dev_langs: TSQL
helpviewer_keywords:
- fn_net_changes_<capture_instance>
- sys.fn_net_changes_<capture_instance>
ms.assetid: 342fa030-9fd9-4b74-ae4d-49f6038a5073
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: be3cd4da4aa890624dc33f36af135bd96dbc3057
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="sysfnnetchangesltcaptureinstancegt-transact-sql"></a>sys.fn_net_changes_&lt;capture_instance&gt; (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  包装**净更改**查询函数。 创建这些函数所必需的脚本由 sys.sp_cdc_generate_wrapper_function 存储过程生成。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
fn_net_changes_<capture_instance> ('start_time', 'end_time', '<row_filter_option>' )  
  
<capture_instance> ::= The name of the capture instance.  
<row_filter_option> ::=  
{ all  
  | all with mask  
  | all with merge  
}  
```  
  
## <a name="arguments"></a>参数  
 *start_time*  
 **Datetime**值，该值表示要包括在结果集中的更改表项的范围的低端点。  
  
 仅在 cdc。 < capture_instance > _CT 行更改表具有严格大于关联的提交时间*start_time*包含在结果集。  
  
 如果为此参数提供 NULL 值，则查询范围的低端点对应于捕获实例的有效范围的低端点。  
  
 *end_time*  
 **Datetime**值，该值表示要包括在结果集中的更改表项的范围的高端点。  
  
 此参数可以采用两种含义，具体取决于为选择的值之一上@closed_high_end_point时调用 sys.sp_cdc_generate_wrapper_function 以生成用于创建包装函数的脚本：  
  
-   @closed_high_end_point = 1  
  
     仅在 cdc。 < capture_instance > _CT 行更改表中具有的值\_ \_$start_lsn 和相应提交时间小于或等于**start_time**包含在结果集。  
  
-   @closed_high_end_point = 0  
  
     仅在 cdc。 < capture_instance > _CT 行更改表中具有的值\_ \_$start_lsn 和相应提交时间严格小于**start_time**包含在结果集。  
  
 如果为此参数提供 NULL 值，则查询范围的高端点对应于捕获实例的有效范围的高端点。  
  
 *< row_filter_option >* :: = {所有 | 所有与掩码 | 全部且具有合并}  
 控制元数据列的内容和结果集中所返回的行的选项。 可以是下列选项之一：  
  
 all  
 返回更改了内容列的某一行的最终内容，以及在元数据列 __CDC_OPERATION 中应用该行所需的操作。  
  
 all with mask  
 返回所有更改了内容列的行的最终内容，以及在元数据列 __CDC_OPERATION 中应用每一行所需的操作。 如果在生成用于创建包装函数的脚本时指定了更新标志列表，则需要使用此选项来填充更新掩码。  
  
 all with merge  
 返回内容列中所有已更改的行的最终内容。  
  
 列 __CDC_OPERATION 将是以下两个值之一：  
  
-   D，如果必须删除该行。  
  
-   M，如果必须插入或更新该行。  
  
 确定是否需要插入或更新以便对目标应用更改的逻辑会增加查询的复杂性。 如果不需要区分插入和更新操作，请使用此选项以提高性能。 此方式在合并操作直接可用的目标环境中效果最好，例如 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 环境。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|列类型|Description|  
|-----------------|-----------------|-----------------|  
|\<中的列@column_list>|**各不相同**|在中标识的列**column_list** sp_cdc_generate_wrapper_function 时被调用以生成用于创建包装的脚本的自变量。 如果*column_list*为 NULL，所有的跟踪的源列将显示在结果集。|  
|__CDC_OPERATION|**nvarchar(2)**|一个操作代码，它指示将行应用于目标环境所需的操作。 自变量的值将因该操作*row_filter_option*提供的、 在下面的调用：<br /><br /> *row_filter_option* = 'all'，'all with mask<br /><br /> 'D' - 删除操作<br /><br /> 'I' - 插入操作<br /><br /> 'UN' - 更新操作<br /><br /> *row_filter_option* = 全部且具有合并<br /><br /> 'D' - 删除操作<br /><br /> 'M' - 插入操作或更新操作|  
|\<中的列@update_flag_list>|**bit**|通过将 _uflag 追加到列名称末尾所命名的位标记。 标志会对非 null 值时，才*row_filter_option* **= all with mask**和\__CDC_OPERATION **= 取消**。 如果在查询窗口中修改相应的列，则会将其设置为 1； 否则为 0。|  
  
## <a name="remarks"></a>注释  
 fn_net_changes_ < capture_instance > 函数充当 cdc.fn_cdc_get_net_changes_<capture_instance> 查询函数的包装。 sys.sp_cdc_generate_wrapper 存储过程用于创建包装的脚本。  
  
 不会自动创建包装函数。 必须做两件事，才能创建包装函数：  
  
1.  运行该存储过程以生成用于创建包装的脚本。  
  
2.  执行该脚本以实际创建包装函数。  
  
 包装器函数使用户能够系统地查询受间隔内发生的更改**datetime** LSN 值通过值而不是。 包装器函数执行之间所提供的所有所需的转换**datetime**值和为查询函数的变量的内部所需的 LSN 值。 当按顺序使用包装函数，来处理更改数据流时，确保没有数据丢失或重复前提是遵循以下约定：@end_time作为提供与一次调用关联间隔的值@start_time与后续调用关联的间隔的值。  
  
 通过在创建脚本时使用 @closed_high_end_point 参数，您可以生成包装以支持指定查询窗口中的闭合上限或开放上限。 就是说，您可以决定其提交时间等于提取间隔的上限的条目是否要包括在间隔中。 默认情况下，包括上限。  
  
 结果集返回**净更改**只跟踪中的列的包装函数返回@column_list时生成包装。 如果 @column_list 为 NULL，则返回所有被跟踪的源列。 源列后面是一个操作列 __CDC_OPERATION，该列包含一个或两个用于标识操作的字符。  
  
 位的标志则会追加到结果集中为每一列的参数中标识@update_flag_list。 有关**净更改**包装，位标志将始终为 NULL，如果@row_filter_option，它是使用包装函数的调用中是 'all' all with merge。 如果@row_filter_option设置为 all with mask，和 __CDC_OPERATION 具有或 I，标志的值也将为 NULL。 如果\__CDC_OPERATION 是取消，该标志将设置为 1 或 0，具体取决于是否**net**更新操作导致对列进行更改。  
  
 变更数据捕获配置模板“实例化架构的 CDC 包装 TVF”显示如何使用 sp_cdc_generate_wrapper_function 存储过程以获取某个架构的已定义查询函数的所有包装函数的 CREATE 脚本。 然后，此模板创建这些脚本。 有关模板的详细信息，请参阅[模板资源管理器](http://msdn.microsoft.com/library/b9ee55c5-bb44-4f76-90ac-792d8d83b4c8)。  
  
## <a name="see-also"></a>另请参阅  
 [sys.sp_cdc_generate_wrapper_function &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60; capture_instance &#62;&#40;Transact SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)  
  
  
