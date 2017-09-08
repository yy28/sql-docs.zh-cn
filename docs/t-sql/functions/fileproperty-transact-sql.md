---
title: "FILEPROPERTY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FILEPROPERTY_TSQL
- FILEPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- viewing file properties
- names [SQL Server], files
- displaying file properties
- file properties [SQL Server]
- FILEPROPERTY function
- file names [SQL Server], FILEPROPERTY
ms.assetid: b82244ed-d623-431f-aa06-8017349d847f
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7078fecb77bad44fd6aa4c3ce0baf9565f1d6d3f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="fileproperty-transact-sql"></a>FILEPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定当前数据库中的文件名和属性名时，返回指定的文件名属性值。 对于不在当前数据库中的文件，返回 NULL。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
FILEPROPERTY ( file_name , property )  
```  
  
## <a name="arguments"></a>参数  
 *文件名*  
 包含与将为之返回属性信息的当前数据库相关联的文件名的表达式。 *file_name*是**nchar(128)**。  
  
 *属性*  
 包含将返回的文件属性名的表达式。 *属性*是**varchar （128)**，和可以是以下值之一。  
  
|值|Description|返回的值|  
|-----------|-----------------|--------------------|  
|**IsReadOnly**|文件组是只读的。|1 = True<br /><br /> 0 = False<br /><br /> NULL = 输入无效。|  
|**IsPrimaryFile**|文件为主文件。|1 = True<br /><br /> 0 = False<br /><br /> NULL = 输入无效。|  
|**IsLogFile**|文件为日志文件。|1 = True<br /><br /> 0 = False<br /><br /> NULL = 输入无效。|  
|**SpaceUsed**|指定的文件使用的空间量。|在文件中分配的页数|  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
## <a name="remarks"></a>注释  
 *file_name*对应于**名称**中的列**sys.master_files**或**sys.database_files**目录视图。  
  
## <a name="examples"></a>示例  
 以下示例返回 `IsPrimaryFile` 数据库中的 `AdventureWorks_Data` 文件名的 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 属性的设置。  
  
```  
  
SELECT FILEPROPERTY('AdventureWorks2012_Data', 'IsPrimaryFile')AS [Primary File];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Primary File   
-------------  
1  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅  
 [FILEGROUPPROPERTY &#40;Transact SQL &#41;](../../t-sql/functions/filegroupproperty-transact-sql.md)   
 [元数据函数 &#40;Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_spaceused (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
