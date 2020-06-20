---
title: 映射 CLR 参数数据 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 70274fcc16caec38d4d960f89fe586b32662dc57
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954767"
---
# <a name="mapping-clr-parameter-data"></a>映射 CLR 参数数据
  下表列出了 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型、它们在公共语言运行时（CLR）中 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in 命名空间中的等效项 `System.Data.SqlTypes` 以及其在 .NET FRAMEWORK 中的本机 CLR 等效项 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 。  
  
||||  
|-|-|-|  
|**SQL Server 数据类型**|类型（在 System.Data.SqlTypes 或 Microsoft.SqlServer.Types 中）|**CLR 数据类型 (.NET Framework)**|  
|`bigint`|`SqlInt64`|**Int64，可以为 Null\<Int64>**|  
|`binary`|`SqlBytes, SqlBinary`|`Byte[]`|  
|`bit`|`SqlBoolean`|**布尔值，可以为 Null\<Boolean>**|  
|`char`|无|无|  
|`cursor`|无|无|  
|`date`|`SqlDateTime`|**DateTime，可以为 Null\<DateTime>**|  
|`datetime`|`SqlDateTime`|**DateTime，可以为 Null\<DateTime>**|  
|`datetime2`|无|**DateTime，可以为 Null\<DateTime>**|  
|`DATETIMEOFFSET`|`None`|**DateTimeOffset，可以为 Null\<DateTimeOffset>**|  
|`decimal`|`SqlDecimal`|**十进制，可以为 Null\<Decimal>**|  
|`float`|`SqlDouble`|**Double，可以为 Null\<Double>**|  
|`geography`|`SqlGeography`<br /><br /> `SqlGeography`是在 Microsoft.SqlServer.Types.dll 中定义的，它与 SQL Server 一起安装，并且可以从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能包](https://www.microsoft.com/download/details.aspx?id=53164)下载。|无|  
|`geometry`|`SqlGeometry`<br /><br /> `SqlGeometry`是在 Microsoft.SqlServer.Types.dll 中定义的，它与 SQL Server 一起安装，并且可以从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能包](https://www.microsoft.com/download/details.aspx?id=53164)下载。|无|  
|`hierarchyid`|`SqlHierarchyId`<br /><br /> `SqlHierarchyId`是在 Microsoft.SqlServer.Types.dll 中定义的，它与 SQL Server 一起安装，并且可以从 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能包](https://www.microsoft.com/download/details.aspx?id=53164)下载。|无|  
|`image`|无|无|  
|`int`|`SqlInt32`|**Int32，可以为 Null\<Int32>**|  
|`money`|`SqlMoney`|**十进制，可以为 Null\<Decimal>**|  
|`nchar`|`SqlChars, SqlString`|`String, Char[]`|  
|`ntext`|无|无|  
|`numeric`|`SqlDecimal`|**十进制，可以为 Null\<Decimal>**|  
|`nvarchar`|`SqlChars, SqlString`<br /><br /> `SQLChars` 更适用于数据传输和访问，而 `SQLString` 更适用于执行字符串运算。|`String, Char[]`|  
|`nvarchar(1), nchar(1)`|`SqlChars, SqlString`|**Char、String、Char []，可以为 Null\<char>**|  
|`real`|`SqlSingle`（`SqlSingle` 的范围，但大于 `real`）|**单个，可以为 Null\<Single>**|  
|`rowversion`|无|`Byte[]`|  
|`smallint`|`SqlInt16`|**Int16，可为 Null\<Int16>**|  
|`smallmoney`|`SqlMoney`|**十进制，可以为 Null\<Decimal>**|  
|`sql_variant`|无|`Object`|  
|`table`|无|无|  
|`text`|无|无|  
|`time`|无|**TimeSpan，可以为 Null\<TimeSpan>**|  
|`timestamp`|无|无|  
|`tinyint`|`SqlByte`|**字节，可以为 Null\<Byte>**|  
|`uniqueidentifier`|`SqlGuid`|**Guid，可以为 Null\<Guid>**|  
|`User-defined type(UDT)`|无|绑定到相同程序集或依赖程序集中的用户定义类型的相同类。|  
|**varbinary**|`SqlBytes, SqlBinary`|`Byte[]`|  
|`varbinary(1), binary(1)`|`SqlBytes, SqlBinary`|**byte、Byte []、可以为 Null\<byte>**|  
|`varchar`|无|无|  
|`xml`|`SqlXml`|无|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>使用 Out 参数的自动数据类型转换  
 通过以 `out` 修饰符 (Microsoft Visual C#) 或 `<Out()> ByRef` (Microsoft Visual Basic) 来标记输入参数，CLR 方法可以将信息返回到发起调用的代码或程序。如果输入参数是 `System.Data.SqlTypes` 命名空间中的 CLR 数据类型，并且发起调用的程序指定其等效 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型作为输入参数，则会在 CLR 方法返回数据类型时自动发生类型转换。  
  
 例如，以下 CLR 存储过程具有以 `SqlInt32` (C#) 或 `out` (Visual Basic) 进行标记的 `<Out()> ByRef` CLR 数据类型的输入参数：  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ ... }  
```  
  
```vb  
<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( <Out()> ByRef value As SqlInt32)  
...  
End Sub  
```  
  
 在数据库中生成和创建程序集之后，将用以下 Transact-SQL 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中创建存储过程，该 Transact-SQL 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型 `int` 作为 OUTPUT 参数：  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 调用 CLR 存储过程时，`SqlInt32` 数据类型将自动转换到 `int` 数据类型，并返回到调用程序。  
  
 但是，并非所有 CLR 数据类型都可以通过 out 参数自动转换到其等效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。 下表列出了这些例外类型。  
  
|||  
|-|-|  
|**CLR 数据类型 (SQL Server)**|**SQL Server 数据类型**|  
|`Decimal`|smallmoney|  
|`SqlMoney`|smallmoney|  
|`Decimal`|money|  
|`DateTime`|smalldatetime|  
|`SQLDateTime`|smalldatetime|  
  
## <a name="change-history"></a>更改历史记录  
  
|更新的内容|  
|---------------------|  
|将 `SqlGeography`、`SqlGeometry` 和 `SqlHierarchyId` 类型添加到了映射表。|  
  
## <a name="see-also"></a>另请参阅  
 [.NET Framework 中的 SQL Server 数据类型](sql-server-data-types-in-the-net-framework.md)  
  
  
