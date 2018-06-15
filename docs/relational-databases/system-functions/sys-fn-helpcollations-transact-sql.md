---
title: sys.fn_helpcollations (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_helpcollations
- fn_helpcollations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_helpcollations function
- collations [SQL Server], supported
- fn_helpcollations function
ms.assetid: b5082e81-1fee-4e2c-b567-5412eaee41c1
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c6b16defc5c6ffc11fc13f59d014502ee37f8398
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33234313"
---
# <a name="sysfnhelpcollations-transact-sql"></a>sys.fn_helpcollations (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  返回所有支持的排序列表。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
fn_helpcollations ()  
```  
  
## <a name="tables-returned"></a>返回的表  
 **fn_helpcollations**返回以下信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|名称|**sysname**|标准排序规则名称|  
|Description|**nvarchar(1000)**|排序规则说明|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持 Windows 排序规则。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还支持有限数量（<80 个）的排序规则（称为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序规则），这些规则是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持的 Windows 排序规则之前开发的。 仍然支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序规则只是为了实现向后兼容性，不应将这些排序规则用于新开发工作。 有关 Windows 排序规则的详细信息，请参阅 [Windows 排序规则名称 (Transact-SQL)](../../t-sql/statements/windows-collation-name-transact-sql.md)。 有关排序规则的详细信息，请参阅[Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)。  
  

## <a name="examples"></a>示例  
 以下示例返回以字母 `L` 开头并且是二进制排序规则的所有排序规则名称。  
  
```  
SELECT Name, Description FROM fn_helpcollations()  
WHERE Name like 'L%' AND Description LIKE '% binary sort';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```   
 Name                   Description  
 -------------------    ------------------------------------  
 Lao_100_BIN            Lao-100, binary sort  
 Latin1_General_BIN     Latin1-General, binary sort  
 Latin1_General_100_BIN Latin1-General-100, binary sort  
 Latvian_BIN            Latvian, binary sort  
 Latvian_100_BIN        Latvian-100, binary sort  
 Lithuanian_BIN         Lithuanian, binary sort  
 Lithuanian_100_BIN     Lithuanian-100, binary sort  
  
 (7 row(s) affected)  
 ```    
  
## <a name="see-also"></a>另请参阅  
[COLLATE (Transact-SQL)](~/t-sql/statements/collations.md)   
[COLLATIONPROPERTY &#40;Transact SQL&#41;](../../t-sql/functions/collation-functions-collationproperty-transact-sql.md)  
[Azure SQL 数据仓库的数据库排序规则支持](https://azure.microsoft.com/blog/database-collation-support-for-azure-sql-data-warehouse-2)  

