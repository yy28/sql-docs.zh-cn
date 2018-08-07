---
title: 数据类型转换（数据库引擎）| Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 37
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: eb22a3686b026382da88fede58cb613834254b96
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39456871"
---
# <a name="data-type-conversion-database-engine"></a>数据类型转换（数据库引擎）
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

在以下情况下，可以转换数据类型：
-   当一个对象的数据移到另一个对象，或两个对象之间的数据进行比较或组合时，数据可能必须从一个对象的数据类型转换为另一个对象的数据类型。  
-   将 [!INCLUDE[tsql](../../includes/tsql-md.md)] 结果列、返回代码或输出参数中的数据移到某个程序变量中时，必须将这些数据从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据类型转换成该变量的数据类型。  
  
在应用程序变量与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 结果集列、返回代码、参数或参数标记之间进行转换时，支持的数据类型转换由数据库 API 定义。
  
## <a name="implicit-and-explicit-conversion"></a>隐式和显式转换
可以隐式或显式转换数据类型。
  
隐式转换对用户不可见。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会自动将数据从一种数据类型转换为另一种数据类型。 例如，将 smallint 与 int 进行比较时，在比较之前，smallint 会被隐式转换为 int。
  
GETDATE() 隐式转换为日期样式 0。 SYSDATETIME() 隐式转换为日期样式 21。
  
显式转换使用 CAST 或 CONVERT 函数。
  
[CAST 和 CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) 函数可将值（局部变量、列或其他表达式）从一种数据类型转换为另一种数据类型。 例如，以下 `CAST` 函数可将数值 `$157.27` 转换为字符串 `'157.27'`：
  
```sql
CAST ( $157.27 AS VARCHAR(10) )  
```  
  
如果希望 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程序代码符合 ISO 标准，请使用 CAST 而不要使用 CONVERT。 如果要利用 CONVERT 中的样式功能，请使用 CONVERT 而不要使用 CAST。
  
以下图例显示了可对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统提供的数据类型执行的所有显式和隐式数据类型转换。 这些包括 xml、bigint 和sql_variant。 不存在对 sql_variant 数据类型的赋值进行的隐式转换，但是存在转换为 sql_variant 的隐式转换。
  
![数据类型转换表](../../t-sql/data-types/media/lrdatahd.png "Data type conversion table")
  
## <a name="data-type-conversion-behaviors"></a>数据类型转换行为
将一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象的数据类型转换为另一种数据类型时，不支持某些隐式和显式数据类型转换。 例如，nchar 值无法被转换为 image 值。 nchar 只能显式转换为 binary，而不支持隐式转换为 binary。 但是，nchar 既可以显式也可以隐式转换为 nvarchar。
  
以下各主题说明各对应数据类型展示的转换行为：
  
 - [binary 和 varbinary (Transact-SQL)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)  
 - [datetime2 (Transact-SQL)](../../t-sql/data-types/datetime2-transact-sql.md)  
 - [money 和 smallmoney (Transact-SQL)](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
 - [bit (Transact-SQL)](../../t-sql/data-types/bit-transact-sql.md)  
 - [datetimeoffset (Transact-SQL)](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
 - [smalldatetime (Transact-SQL)](../../t-sql/data-types/smalldatetime-transact-sql.md)  
 - [char 和 varchar (Transact-SQL)](../../t-sql/data-types/char-and-varchar-transact-sql.md)  
 - [decimal 和 numeric (Transact-SQL)](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)  
 - [sql_variant (Transact-SQL)](../../t-sql/data-types/sql-variant-transact-sql.md)  
 - [date (Transact-SQL)](../../t-sql/data-types/date-transact-sql.md)  
 - [float 和 real (Transact-SQL)](../../t-sql/data-types/float-and-real-transact-sql.md)  
 - [time (Transact-SQL)](../../t-sql/data-types/time-transact-sql.md)  
 - [datetime (Transact-SQL)](../../t-sql/data-types/datetime-transact-sql.md)  
 - [int、bigint、smallint 和 tinyint (Transact-SQL)](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
 - [uniqueidentifier (Transact-SQL)](../../t-sql/data-types/uniqueidentifier-transact-sql.md)  
  
###  <a name="converting-data-types-by-using-ole-automation-stored-procedures"></a>使用 OLE 自动化存储过程转换数据类型  
由于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 数据类型，而 OLE 自动化使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 数据类型，因此 OLE 自动化存储过程必须转换在两者之间传递的数据。
  
下表说明了从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 到 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 的数据类型转换。
  
|SQL Server 数据类型|Visual Basic 数据类型|  
|--------------------------|----------------------------|  
|**char**、**varchar**、**text**、**nvarchar**、**ntext**|**String**|  
|**decimal**、**numeric**|**String**|  
|**bit**|**Boolean**|  
|**binary**、**varbinary**、**image**|一维 Byte() 数组|  
|**int**|**Long**|  
|**smallint**|**Integer**|  
|**tinyint**|**Byte**|  
|**float**|**双精度**|  
|**real**|**Single**|  
|**money**、 **smallmoney**|**货币**|  
|**datetime**、**smalldatetime**|**Date**|  
|设置为 NULL 的任何类型|Variant 设置为 Null|  
  
除了 binary、varbinary 和 image 值以外，所有单个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 值都被转换为单个 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 值。 这些值将被转换为 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 中的一维 Byte() 数组。 此数组的范围为 Byte（0 到长度 1），其中长度是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] binary、varbinary 或 image 值中的字节数。
  
以下是从 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 数据类型到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型的转换。
  
|Visual Basic 数据类型|SQL Server 数据类型|  
|----------------------------|--------------------------|  
|**Long**、**Integer**、**Byte**、**Boolean**、**Object**|**int**|  
|**Double**、**Single**|**float**|  
|**货币**|**money**|  
|**Date**|**datetime**|  
|小于或等于 4000 个字符的 String|**varchar**/**nvarchar**|  
|大于 4000 个字符的 String|**text**/**ntext**|  
|小于或等于 8000 字节的一维 Byte() 数组|**varbinary**|  
|大于 8000 字节的一维 Byte() 数组|**图像**|  
  
## <a name="see-also"></a>另请参阅
[OLE 自动存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
[CAST 和 CONVERT (Transact-SQL)](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)  
[COLLATE (Transact-SQL)](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)
  
  
