---
title: sys.sp_cdc_generate_wrapper_function (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_generate_wrapper_function_TSQL
- sp_cdc_generate_wrapper_function
- sys.sp_cdc_generate_wrapper_function_TSQL
- sys.sp_cdc_generate_wrapper_function
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_generate_wrapper_function
- sp_cdc_generate_wrapper_function
ms.assetid: 85bc086d-8a4e-4949-a23b-bf53044b925c
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0ea44e7c2d9ca4f56d401688aa496aa851e563fe
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47780395"
---
# <a name="sysspcdcgeneratewrapperfunction-transact-sql"></a>sys.sp_cdc_generate_wrapper_function (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  生成相应的脚本，为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中可用的变更数据捕获查询函数创建包装函数。 所生成的包装中支持的 API 使查询间隔能够指定为 datetime 间隔。 这使该函数能够很好地应用于许多仓库应用程序，包括那些由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包设计器开发的应用程序，这些设计器使用变更数据捕获技术来确定增量加载。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_cdc_generate_wrapper_function  
    [ [ @capture_instance sysname = ] 'capture_instance'  
    [ , [ @closed_high_end_point = ] closed_high_end_pt  
    [ , [ @column_list = ] 'column_list'  
```  
  
```  
  
[ , [ @update_flag_list = ] 'update_flag_list'  
```  
  
## <a name="arguments"></a>参数  
 [ @capture_instance=] '*capture_instance*  
 要为其生成脚本的捕获实例。 *capture_instance*是**sysname**并且具有默认值为 NULL。 如果不指定值，或将值显式设置为 NULL，则会为所有捕获实例生成包装脚本  
  
 [ @closed_high_end_point=] *high_end_pt_flag*  
 一个标志位，指示生成的过程是否将提交时间等于高端点的更改包括在提取间隔内。 *high_end_pt_flag*是**位**和具有默认值为 1，指示应包括端点。 值为 0 表示所有提交时间将严格小于高端点。  
  
 [ @column_list=] '*column_list*  
 将包括在由包装函数返回的结果集中的捕获列的列表。 *column_list*是**nvarchar （max)** 并且具有默认值为 NULL。 指定 NULL 时，将包括所有捕获列。  
  
 [ @update_flag_list=] '*update_flag_list*  
 包含的列的列表，在由包装函数返回的结果集中将为这些列包括一个更新标志。 *update_flag_list*是**nvarchar （max)** 并且具有默认值为 NULL。 指定 NULL 时，不包括更新标志。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|列类型|Description|  
|-----------------|-----------------|-----------------|  
|**function_name**|**nvarchar(145)**|生成的函数的名称。|  
|**create_script**|**nvarchar(max)**|创建捕获实例包装函数的脚本。|  
  
## <a name="remarks"></a>备注  
 将总是生成为捕获实例创建包装所有更改查询的函数的脚本。 如果捕获实例支持净更改查询，也会生成为此查询生成包装的脚本。  
  
## <a name="examples"></a>示例  
 以下示例演示如何使用 `sys.sp_cdc_generate_wrapper_function` 为所有变更数据捕获函数创建包装。  
  
```  
DECLARE @wrapper_functions TABLE (  
    function_name sysname,  
    create_script nvarchar(max));  
  
INSERT INTO @wrapper_functions  
EXEC sys.sp_cdc_generate_wrapper_function;  
  
DECLARE @create_script nvarchar(max);  
DECLARE #hfunctions CURSOR LOCAL fast_forward  
FOR   
    SELECT create_script FROM @wrapper_functions;  
  
OPEN #hfunctions;  
FETCH #hfunctions INTO @create_script;  
WHILE (@@fetch_status <> -1)  
BEGIN  
    EXEC sp_executesql @create_script  
    FETCH #hfunctions INTO @create_script  
END;  
  
CLOSE #hfunctions;  
DEALLOCATE #hfunctions;  
```  
  
## <a name="see-also"></a>请参阅  
 [更改数据捕获存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [变更数据捕获&#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md)  
  
  
