---
title: 映射 CLR 参数数据 |Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlBinary data type
- SqlInt16 data type
- SqlMoney data type
- SqlString data type
- SqlSingle data type
- data types [CLR integration]
- SqlInt64 data type
- SqlDateTime data type
- SqlXml data type
- SqlBoolean data type
- SqlDecimal data type
- SqlBytes data type
- mapping data types [CLR integration]
- SqlChars data type
- SqlInt32 data type
ms.assetid: 89b43ee9-b9ad-4281-a4bf-c7c8d116daa2
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8c9cfd87578b2ffaaefb8b46b340f76f74b373ed
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47794557"
---
# <a name="mapping-clr-parameter-data"></a>映射 CLR 参数数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  下表列出[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型，公共语言运行时 (CLR) 为中的等效项[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中**System.Data.SqlTypes**命名空间，在及其本机CLR等效项[!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET framework。  
  
||||  
|-|-|-|  
|**SQL Server 数据类型**|类型（在 System.Data.SqlTypes 或 Microsoft.SqlServer.Types 中）|**CLR 数据类型 (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64，可以为 Null\<Int64 >**|  
|**binary**|**SqlBytes SqlBinary**|**Byte[]**|  
|**bit**|**SqlBoolean**|**布尔值、 可以为 Null\<布尔 >**|  
|**char**|None|None|  
|**cursor**|None|None|  
|**date**|**SqlDateTime**|**日期时间，可以为 Null\<日期时间 >**|  
|**datetime**|**SqlDateTime**|**日期时间，可以为 Null\<日期时间 >**|  
|**datetime2**|None|**日期时间，可以为 Null\<日期时间 >**|  
|DATETIMEOFFSET|**无**|**DateTimeOffset，可以为 Null\<DateTimeOffset >**|  
|**decimal**|**SqlDecimal**|**Decimal、 可以为 Null\<十进制 >**|  
|**float**|**SqlDouble**|**双精度，可以为 Null\<双精度 >**|  
|**地理**|**SqlGeography**<br /><br /> **SqlGeography** Microsoft.SqlServer.Types.dll 中定义，这与 SQL Server 安装，可以从下载[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][功能包](https://www.microsoft.com/download/details.aspx?id=52676)。|None|  
|**geometry**|**SqlGeometry**<br /><br /> **SqlGeometry** Microsoft.SqlServer.Types.dll 中定义，这与 SQL Server 安装，可以从下载[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][功能包](https://www.microsoft.com/download/details.aspx?id=52676)。|None|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId** Microsoft.SqlServer.Types.dll 中定义，这与 SQL Server 安装，可以从下载[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][功能包](https://www.microsoft.com/download/details.aspx?id=52676)。|None|  
|**image**|None|None|  
|**int**|**SqlInt32**|**Int32 类型，可以为 Null\<Int32 >**|  
|**money**|**SqlMoney**|**Decimal、 可以为 Null\<十进制 >**|  
|**nchar**|**SqlChars SqlString**|**String，Char]**|  
|**ntext**|None|None|  
|**numeric**|**SqlDecimal**|**Decimal、 可以为 Null\<十进制 >**|  
|**nvarchar**|**SqlChars SqlString**<br /><br /> **SQLChars**更好的匹配的数据传输和访问权限，并**SQLString**是执行字符串操作的更好的匹配项。|**String，Char]**|  
|**nvarchar(1)、 nchar(1)**|**SqlChars SqlString**|**Char、 字符串、 Char []，可以为 Null\<char >**|  
|**real**|**SqlSingle** (的范围**SqlSingle**，但是，大于**实际**)|**单一的可以为 Null\<单一 >**|  
|**rowversion**|None|**Byte[]**|  
|**smallint**|**SqlInt16**|**Int16，可以为 Null\<Int16 >**|  
|**smallmoney**|**SqlMoney**|**Decimal、 可以为 Null\<十进制 >**|  
|**sql_variant**|None|**对象**|  
|**table**|None|None|  
|**text**|None|None|  
|**time**|None|**TimeSpan，可以为 Null\<TimeSpan >**|  
|**timestamp**|None|None|  
|**tinyint**|**以**|**字节，可以为 Null\<字节 >**|  
|**uniqueidentifier**|**SqlGuid**|**Guid，可以为 Null\<Guid >**|  
|**用户定义 type(UDT)**|None|绑定到相同程序集或依赖程序集中的用户定义类型的相同类。|  
|**varbinary**|**SqlBytes SqlBinary**|**Byte[]**|  
|**varbinary(1)、 binary(1)**|**SqlBytes SqlBinary**|**字节、 Byte []，可以为 Null\<字节 >**|  
|**varchar**|None|None|  
|**xml**|**SqlXml**|None|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>使用 Out 参数的自动数据类型转换  
 CLR 方法可以通过将标记与输入的参数向调用代码或程序返回的信息**出**修饰符 (Microsoft Visual C#) 或 **\<out （) > ByRef** (Microsoft Visual Basic)如果输入的参数是中的 CLR 数据类型**System.Data.SqlTypes**命名空间，并且调用程序指定其等效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型作为输入参数，自动发生类型转换当 CLR 方法返回的数据类型。  
  
 例如，以下 CLR 存储过程具有输入的参数的**SqlInt32** CLR 数据类型将标有**out** (C#) 或 **\<out （) > ByRef** (Visual Basic 中):  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ … }  
```  
  
```vb  
\<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( \<Out()> ByRef value As SqlInt32)  
…  
End Sub  
```  
  
 生成并在数据库中创建程序集后，在创建此存储的过程[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用以下 TRANSACT-SQL，它指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型**int**作为输出参数：  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 CLR 存储调用过程时， **SqlInt32**数据类型自动转换为**int**数据类型，并返回到调用程序。  
  
 但是，并非所有 CLR 数据类型都可以通过 out 参数自动转换到其等效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。 下表列出了这些例外类型。  
  
|||  
|-|-|  
|**CLR 数据类型 (SQL Server)**|**SQL Server 数据类型**|  
|**十进制**|SMALLMONEY|  
|**SqlMoney**|SMALLMONEY|  
|**十进制**|money|  
|**DateTime**|smalldatetime|  
|**SQLDateTime**|smalldatetime|  
  
## <a name="change-history"></a>更改历史记录  
  
|更新的内容|  
|---------------------|  
|添加**SqlGeography**， **SqlGeometry**，并**SqlHierarchyId**映射表的类型。|  
  
## <a name="see-also"></a>请参阅  
 [.NET Framework 中的 SQL Server 数据类型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
