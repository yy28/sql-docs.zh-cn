---
title: sys. fn_trace_gettable （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_trace_gettable
- fn_trace_gettable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_trace_gettable function
- sys.fn_trace_gettable function
ms.assetid: c2590159-6ec5-4510-81ab-e935cc4216cd
author: rothja
ms.author: jroth
ms.openlocfilehash: 18a6225bca9539f10c4dfea61e99d147cb188d4c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68059225"
---
# <a name="sysfn_trace_gettable-transact-sql"></a>sys.fn_trace_gettable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  以表格形式返回一个或多个跟踪文件的内容。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 请改用扩展事件。  
   
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
fn_trace_gettable ( 'filename' , number_files )  
```  
  
## <a name="arguments"></a>参数  
 "*filename*"  
 指定要读取的初始跟踪文件。 *filename*为**nvarchar （256）**，无默认值。  
  
 *number_files*  
 指定要读取的滚动更新文件数。 此数目包括*filename*中指定的初始文件。 *number_files*是**int**。  
  
## <a name="remarks"></a>备注  
 如果*number_files*指定为**默认值**，则**fn_trace_gettable**将读取所有滚动更新文件，直到到达跟踪结尾为止。 **fn_trace_gettable**返回一个表，该表包含指定跟踪的所有有效列。 有关详细信息，请参阅[&#40;transact-sql&#41;sp_trace_setevent ](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)。  
  
 请注意，fn_trace_gettable 函数将不会加载滚动更新文件（使用*number_files*参数指定此选项时），其中原始跟踪文件名以下划线和数值结尾。 （这不适用于在滚动文件时自动追加的下划线和数字。）作为一种解决方法，您可以重命名跟踪文件以删除原始文件名中的下划线。 例如，如果原始文件命名为**Trace_Oct_5 trace.dat.trc** ，并且滚动更新文件的 Trace_Oct_5_1 名称为**trace.dat.trc**，则可以将文件重命名为**TraceOct5** **TraceOct5_1 和 trace.dat.trc**。  
  
 该函数可以读取在执行该函数所在实例中仍处于活动状态的跟踪。  
  
## <a name="permissions"></a>权限  
 要求对服务器具有 ALTER TRACE 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-fn_trace_gettable-to-import-rows-from-a-trace-file"></a>A. 使用 fn_trace_gettable 从跟踪文件导入行  
 下面的示例在 `fn_trace_gettable` 语句的 `FROM` 子句内部调用 `SELECT...INTO`。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * INTO temp_trc  
FROM fn_trace_gettable('c:\temp\mytrace.trc', default);  
GO  
```  
  
### <a name="b-using-fn_trace_gettable-to-return-a-table-with-an-identity-column-that-can-be-loaded-into-a-sql-server-table"></a>B. 使用 fn_trace_gettable 返回一个表，其中具有可以加载到 SQL Server 表中的 IDENTITY 列  
 以下示例在 `SELECT...INTO` 语句中调用该函数，并返回一个表，其中具有可加载到表 `IDENTITY` 中的 `temp_trc` 列。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT IDENTITY(int, 1, 1) AS RowNumber, * INTO temp_trc  
FROM fn_trace_gettable('c:\temp\mytrace.trc', default);  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_trace_generateevent &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
  
