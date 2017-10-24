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
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 166a85e5fe33a95cd8a36f221c2a774e4a0a9fb2
ms.contentlocale: zh-cn
ms.lasthandoff: 10/24/2017

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
|**CodePage**|排序规则的非 Unicode 代码页。 请参阅[附录 G DBCS/Unicode 映射表](https://msdn.microsoft.com/en-us/library/cc194886.aspx)和[附录 H 代码页](https://msdn.microsoft.com/en-us/library/cc195051.aspx)转换这些值，并查看其字符映射。|  
|**LCID**|排序规则的 Windows LCID。 请参阅[LCID 结构](https://msdn.microsoft.com/en-us/library/cc233968.aspx)转换这些值 (将需要将转换为`VARBINARY`第一个)。|  
|**ComparisonStyle**|排序规则的 Windows 比较样式。 对于所有的二进制排序规则，则返回 0 (同时`_BIN`和`_BIN2`) 以及当所有属性都是敏感。 位掩码值：<br /><br /> 忽略大小写： 1<br /><br /> 忽略重音： 2<br /><br /> 忽略假名： 65536<br /><br /> 忽略宽度： 131072|  
|**版本**|从排序规则 ID 的版本字段派生的排序规则版本。 返回一个整数值 0 到 3 之间。<br /><br /> 使用"140"名称中的排序规则返回 3。<br /><br /> 排序规则与名称中的"100"返回 2。<br /><br /> 排序规则与名称中的"90"返回 1。<br /><br /> 所有其他排序规则均返回 0。|  
  
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
  
  


