---
title: "数据类型转换 （数据库引擎） |Microsoft 文档"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- converting data types [SQL Server]
- CONVERT function
- data types [SQL Server], converting
- implicit data type conversions
- explicit data type conversions [SQL Server]
- converting data types [SQL Server], about converting data types
ms.assetid: ffacf45e-a488-48d0-9bb0-dcc7fd365299
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 811eacd3dc0cbbd622fc6eac6ad91a6e740554f4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="data-type-conversion-database-engine"></a>数据类型转换 （数据库引擎）
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

在以下情况下，可以转换数据类型：
-   当一个对象的数据移到另一个对象，或两个对象之间的数据进行比较或组合时，数据可能必须从一个对象的数据类型转换为另一个对象的数据类型。  
-   当从数据[!INCLUDE[tsql](../../includes/tsql-md.md)]结果列，返回代码或输出参数将被移动到程序变量，因此必须从转换数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]系统数据类型设置为变量的数据类型。  
  
在应用程序变量与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 结果集列、返回代码、参数或参数标记之间进行转换时，支持的数据类型转换由数据库 API 定义。
  
## <a name="implicit-and-explicit-conversion"></a>隐式和显式转换
可以隐式或显式转换数据类型。
  
隐式转换对用户不可见。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会自动将数据从一种数据类型转换为另一种数据类型。 例如，当**smallint**与相比**int**、 **smallint**隐式转换为**int**在进行比较之前继续进行。
  
**Getdate （） 函数**隐式转换为日期样式 0。 **SYSDATETIME()**隐式转换为日期样式 21。
  
显式转换使用 CAST 或 CONVERT 函数。
  
[CAST 和 CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md)函数将从一种数据类型 （本地变量、 列或另一个表达式） 的值转换为另一个。 例如，以下 `CAST` 函数可将数值 `$157.27` 转换为字符串 `'157.27'`：
  
```sql
CAST ( $157.27 AS VARCHAR(10) )  
```  
  
如果希望 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程序代码符合 ISO 标准，请使用 CAST 而不要使用 CONVERT。 如果要利用 CONVERT 中的样式功能，请使用 CONVERT 而不要使用 CAST。
  
以下图例显示了可对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统提供的数据类型执行的所有显式和隐式数据类型转换。 其中包括**xml**， **bigint**，和**sql_variant**。 在从分配上没有隐式转换**sql_variant**数据类型，但没有隐式转换为**sql_variant**。
  
![数据类型转换表](../../t-sql/data-types/media/lrdatahd.png "数据类型转换表")
  
## <a name="data-type-conversion-behaviors"></a>数据类型转换行为
将一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象的数据类型转换为另一种数据类型时，不支持某些隐式和显式数据类型转换。 例如， **nchar**无法将值转换为**映像**值。 **Nchar**仅可以转换为**二进制**通过使用显式转换，隐式转换为**二进制**不支持。 但是， **nchar**可以显式或隐式转换为**nvarchar**。
  
以下各主题说明各对应数据类型展示的转换行为：
  
 - [binary 和 varbinary (Transact-SQL)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)  
 - [datetime2 (Transact-SQL)](../../t-sql/data-types/datetime2-transact-sql.md)  
 - [money 和 smallmoney &#40;Transact SQL &#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
 - [位 &#40;Transact SQL &#41;](../../t-sql/data-types/bit-transact-sql.md)  
 - [datetimeoffset (Transact-SQL)](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
 - [smalldatetime &#40;Transact SQL &#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)  
 - [char 和 varchar (Transact-SQL)](../../t-sql/data-types/char-and-varchar-transact-sql.md)  
 - [小数和数值 &#40;Transact SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)  
 - [sql_variant (Transact-SQL)](../../t-sql/data-types/sql-variant-transact-sql.md)  
 - [date (Transact-SQL)](../../t-sql/data-types/date-transact-sql.md)  
 - [float 和 real &#40;Transact SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
 - [时间 &#40;Transact SQL &#41;](../../t-sql/data-types/time-transact-sql.md)  
 - [datetime &#40;Transact SQL &#41;](../../t-sql/data-types/datetime-transact-sql.md)  
 - [int、 bigint、 smallint 和 tinyint &#40;Transact SQL &#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
 - [uniqueidentifier &#40;Transact SQL &#41;](../../t-sql/data-types/uniqueidentifier-transact-sql.md)  
  
###  <a name="converting-data-types-by-using-ole-automation-stored-procedures"></a>转换数据类型，通过使用 OLE 自动化存储过程  
由于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 数据类型，而 OLE 自动化使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 数据类型，因此 OLE 自动化存储过程必须转换在两者之间传递的数据。
  
下表说明了从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 到 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 的数据类型转换。
  
|SQL Server 数据类型|Visual Basic 数据类型|  
|--------------------------|----------------------------|  
|**char**， **varchar**，**文本**， **nvarchar**， **ntext**|**字符串**|  
|**十进制**，**数值**|**字符串**|  
|**bit**|**Boolean**|  
|**二进制**， **varbinary**，**映像**|一维**byte （)**数组|  
|**int**|**Long**|  
|**int**|**Integer**|  
|**tinyint**|**字节**|  
|**float**|**双精度**|  
|**real**|**Single**|  
|**money**、 **smallmoney**|**货币**|  
|**datetime**， **smalldatetime**|**日期**|  
|设置为 NULL 的任何类型|**Variant**设置为 Null|  
  
所有单个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]值转换为单个[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]值除外**二进制**， **varbinary**，和**映像**值。 这些值转换为一维**byte （)**数组中[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]。 此数组有一系列**字节 (**0 到*长度*1**)**其中*长度*是中的字节数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **二进制**， **varbinary**，或**映像**值。
  
以下是从 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 数据类型到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型的转换。
  
|Visual Basic 数据类型|SQL Server 数据类型|  
|----------------------------|--------------------------|  
|**长**，**整数**，**字节**，**布尔**，**对象**|**int**|  
|**Double**，**单个**|**float**|  
|**货币**|**money**|  
|**日期**|**datetime**|  
|**字符串**4000 个字符或更少|**varchar**/**nvarchar**|  
|**字符串**超过 4000 个字符|**文本**/**ntext**|  
|一维**byte （)**数组与 8000 个字节或更少|**varbinary**|  
|一维**byte （)**与多个 8000 个字节的数组|**image**|  
  
## <a name="see-also"></a>另请参阅
[OLE 自动存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[COLLATE &#40;Transact SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)
  
  
