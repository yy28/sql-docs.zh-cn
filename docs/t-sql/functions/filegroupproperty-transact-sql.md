---
title: FILEGROUPPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- FILEGROUPPROPERTY_TSQL
- FILEGROUPPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- filegroups [SQL Server], property values
- FILEGROUPPROPERTY function
- viewing filegroup properties
- displaying filegroup properties
ms.assetid: b3a930e6-df05-4034-929c-f681f5f6fc6e
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: afc112a5e07197ed8b0056a7daeddb55c0c418c9
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2018
ms.locfileid: "37790140"
---
# <a name="filegroupproperty-transact-sql"></a>FILEGROUPPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供文件组和属性名时，返回指定的文件组属性值。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
FILEGROUPPROPERTY ( filegroup_name , property )  
```  
  
## <a name="arguments"></a>参数  
 filegroup_name  
 类型为 sysname 的表达式，它表示要为之返回指定属性信息的文件组名称。  
  
 property  
 类型为 varchar(128) 的表达式，它包含要返回的文件组属性的名称。 property 可以为下列值之一。  
  
|ReplTest1|描述|返回的值|  
|-----------|-----------------|--------------------|  
|**IsReadOnly**|文件组是只读的。|1 = True<br /><br /> 0 = False<br /><br /> NULL = 输入无效。|  
|**IsUserDefinedFG**|文件组是用户定义文件组。|1 = True<br /><br /> 0 = False<br /><br /> NULL = 输入无效。|  
|**IsDefault**|文件组是默认的文件组。|1 = True<br /><br /> 0 = False<br /><br /> NULL = 输入无效。|  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
## <a name="remarks"></a>Remarks  
 filegroup_name 与 sys.filegroups 目录视图中的 name 列相对应。  
  
## <a name="examples"></a>示例  
 此示例返回 `IsDefault` 数据库中主文件组的 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 属性的设置。  
  
```  
  
SELECT FILEGROUPPROPERTY('PRIMARY', 'IsDefault') AS 'Default Filegroup';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Default Filegroup   
---------------------   
1  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另请参阅  
 [FILEGROUP_ID (Transact-SQL)](../../t-sql/functions/filegroup-id-transact-sql.md)   
 [FILEGROUP_NAME (Transact-SQL)](../../t-sql/functions/filegroup-name-transact-sql.md)   
 [元数据函数 (Transact-SQL)](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [sys.filegroups (Transact-SQL)](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)  
  
  
