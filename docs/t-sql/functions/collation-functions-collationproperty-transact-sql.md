---
title: "COLLATIONPROPERTY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLLATIONPROPERTY_TSQL
- COLLATIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], properties
- COLLATIONPROPERTY function
ms.assetid: f5029e74-a1db-4f69-b0f5-5ee920c3311d
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 94cbf96a25a84af1eddce9d94555be9c558c3470
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="collation-functions---collationproperty-transact-sql"></a>排序规则函数-COLLATIONPROPERTY (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中指定排序规则的属性。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
COLLATIONPROPERTY( collation_name , property )  
```  
  
## <a name="arguments"></a>参数  
*collation_name*  
排序规则的名称。 *collation_name*是**nvarchar （128)**，并具有无默认值。
  
*属性*  
排序规则的属性。 *属性*是**varchar （128)**，并且可以是以下值之一：
  
|属性名称|Description|  
|---|---|
|**CodePage**|排序规则的非 Unicode 代码页。|  
|**LCID**|排序规则的 Windows LCID。|  
|**ComparisonStyle**|排序规则的 Windows 比较样式。 对于所有的二进制排序规则，则返回 0。|  
|**版本**|从排序规则 ID 的版本字段派生的排序规则版本。 返回 2、1 或 0。<br /><br /> 名称中含有“100”的排序规则返回 2。<br /><br /> 使用"90"名称中的排序规则） 返回 1。<br /><br /> 所有其他排序规则均返回 0。|  
  
## <a name="return-types"></a>返回类型
**sql_variant**
  
## <a name="examples"></a>示例  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage')  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
## <a name="see-also"></a>另请参阅
[sys.fn_helpcollations (Transact-SQL)](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
  
  


