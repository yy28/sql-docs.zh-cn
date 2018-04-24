---
title: COLLATIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 76baefbaf0fc156d782c705e8a81683770bedc68
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="collation-functions---collationproperty-transact-sql"></a>排序规则函数 - COLLATIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

返回 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中指定排序规则的属性。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
COLLATIONPROPERTY( collation_name , property )  
```  
  
## <a name="arguments"></a>参数  
*collation_name*  
排序规则的名称。 collation_name 的数据类型为 nvarchar(128)，且无默认值。
  
property  
排序规则的属性。 property 的数据类型为 varchar(128)，可以是下列任何值之一：
  
|属性名称|Description|  
|---|---|
|**CodePage**|排序规则的非 Unicode 代码页。 请参阅 [Appendix G DBCS/Unicode Mapping Tables](https://msdn.microsoft.com/en-us/library/cc194886.aspx)（附录 G DBCS/Unicode 映射表）和 [Appendix H Code Pages](https://msdn.microsoft.com/en-us/library/cc195051.aspx)（附录 H 代码页）以转换这些值，并查看它们的字符映射。|  
|**LCID**|排序规则的 Windows LCID。 请参阅 [LCID Structure](https://msdn.microsoft.com/en-us/library/cc233968.aspx)（LCID 结构）以转换这些值（需要先转换为 varbinary）。|  
|**ComparisonStyle**|排序规则的 Windows 比较样式。 对于所有二进制排序规则（(\_BIN) 和 (\_BIN2)），以及需区分所有属性时，返回 0。 位掩码值：<br /><br /> 忽略大小写：1<br /><br /> 忽略重音：2<br /><br /> 忽略假名：65536<br /><br /> 忽略宽度：131072<br /><br /> 注意：尽管会影响比较行为，但此值中不会显示区分变体选择符 (\_VSS) 选项。|  
|**版本(Version)**|从排序规则 ID 的版本字段派生的排序规则版本。 返回一个介于 0 到 3 之间的整数值。<br /><br /> 名称中含有“140”的排序规则返回 3。<br /><br /> 名称中含有“100”的排序规则返回 2。<br /><br /> 名称中含有“90”的排序规则返回 1。<br /><br /> 所有其他排序规则均返回 0。|  
  
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
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
```sql
SELECT COLLATIONPROPERTY('Traditional_Spanish_CS_AS_KS_WS', 'CodePage')  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1252   
```  
  
## <a name="see-also"></a>另请参阅
[sys.fn_helpcollations (Transact-SQL)](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)
  
  

