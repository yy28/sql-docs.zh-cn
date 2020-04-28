---
title: 映射 CLR 参数数据 |Microsoft Docs
description: 本文列出了 Microsoft SQL Server 数据类型、CLR 中用于 SQL Server 的等效项和 .NET Framework 中的本机 CLR 等效项。
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
ms.openlocfilehash: 360a94229b107e9f24bb2a769157c75cdeb3c143
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488448"
---
# <a name="mapping-clr-parameter-data"></a>映射 CLR 参数数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  下[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表列出了**SqlTypes**命名空间中的数据类型、其在公共语言运行时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （CLR）中的等效项以及其在[!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 中的本机 CLR 等效项。  
  
||||  
|-|-|-|  
|**SQL Server 数据类型**|类型（在 System.Data.SqlTypes 或 Microsoft.SqlServer.Types 中）|**CLR 数据类型 (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64，可以\<为 null 的 int64>**|  
|**binary**|**SqlBytes、SqlBinary**|**Byte []**|  
|**bit**|**SqlBoolean**|**布尔值，\<可以为 null 的布尔>**|  
|**char**|无|无|  
|**cursor**|无|无|  
|**date**|**SqlDateTime**|**DateTime、可以\<为 null 的 datetime>**|  
|**datetime**|**SqlDateTime**|**DateTime、可以\<为 null 的 datetime>**|  
|**datetime2**|无|**DateTime、可以\<为 null 的 datetime>**|  
|**DATETIMEOFFSET**|**无**|**DateTimeOffset、可以\<为 null 的 datetimeoffset>**|  
|**decimal**|**SqlDecimal**|**十进制，可以\<为 null 的十进制>**|  
|**float**|**SqlDouble**|**Double，可以\<为 null 的双精度>**|  
|**geography**|**SqlGeography**<br /><br /> **SqlGeography**是在中定义的，后者随 SQL Server 一起安装，并且可以从[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能包](https://www.microsoft.com/download/details.aspx?id=52676)下载。|无|  
|**geometry**|**SqlGeometry**<br /><br /> **SqlGeometry**是在中定义的，后者随 SQL Server 一起安装，并且可以从[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能包](https://www.microsoft.com/download/details.aspx?id=52676)下载。|无|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId**是在中定义的，后者随 SQL Server 一起安装，并且可以从[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [功能包](https://www.microsoft.com/download/details.aspx?id=52676)下载。|无|  
|**图像**|无|无|  
|**int**|**SqlInt32**|**Int32，可以\<为 null 的 int32>**|  
|**money**|**SqlMoney**|**十进制，可以\<为 null 的十进制>**|  
|**nchar**|**SqlChars、SqlString**|**String、Char []**|  
|**ntext**|无|无|  
|**numeric**|**SqlDecimal**|**十进制，可以\<为 null 的十进制>**|  
|**nvarchar**|**SqlChars、SqlString**<br /><br /> **SQLChars**是用于数据传输和访问的更好的匹配项， **SQLString**是用于执行字符串操作的更好的匹配项。|**String、Char []**|  
|**nvarchar （1）、nchar （1）**|**SqlChars、SqlString**|**Char、String、Char []、可以\<为 null 的 char>**|  
|**real**|**SqlSingle** （但是， **SqlSingle**的范围大于**real**）|**单个、可以\<为 null 的单一>**|  
|**rowversion**|无|**Byte []**|  
|**smallint**|**SqlInt16**|**Int16，可\<为 null 的 int16>**|  
|**smallmoney**|**SqlMoney**|**十进制，可以\<为 null 的十进制>**|  
|**sql_variant**|无|**对象**|  
|**table**|无|无|  
|**text**|无|无|  
|**time**|无|**TimeSpan，可\<为 null 的 timespan>**|  
|**timestamp**|无|无|  
|**tinyint**|**SqlByte**|**字节，可以\<为 null 的字节>**|  
|**uniqueidentifier**|**SqlGuid**|**Guid，可\<为 null 的 guid>**|  
|**用户定义的类型（UDT）**|无|绑定到相同程序集或依赖程序集中的用户定义类型的相同类。|  
|**varbinary**|**SqlBytes、SqlBinary**|**Byte []**|  
|**varbinary （1），binary （1）**|**SqlBytes、SqlBinary**|**byte、Byte []、可以\<为 null 的字节>**|  
|**varchar**|无|无|  
|**xml**|**SqlXml**|无|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>使用 Out 参数的自动数据类型转换  
 如果输入参数是系统中的 CLR 数据类型，clr 方法可以通过使用**out**修饰符（microsoft Visual c #）或** \<out （） > ByRef** （microsoft Visual Basic）将输入参数标记为调用代码或程序 **。 SqlTypes**命名空间，并且调用程序将其等效[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的数据类型指定为输入参数，当 CLR 方法返回数据类型时，将自动发生类型转换。  
  
 例如，以下 clr 存储过程具有一个输入参数，其**SqlInt32** CLR 数据类型标记有**out** （c #）或** \<out （） > ByRef** （Visual Basic）：  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ ... }  
```  
  
```vb  
\<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( \<Out()> ByRef value As SqlInt32)  
...  
End Sub  
```  
  
 在数据库中生成并创建了程序集之后，将在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建存储过程，其中包含以下 transact-sql，后者将[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **INT**数据类型指定为 OUTPUT 参数：  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 调用 CLR 存储过程时， **SqlInt32**数据类型会自动转换为**int**数据类型并返回给调用程序。  
  
 但是，并非所有 CLR 数据类型都可以通过 out 参数自动转换到其等效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。 下表列出了这些例外类型。  
  
|||  
|-|-|  
|**CLR 数据类型 (SQL Server)**|**SQL Server 数据类型**|  
|十进制 |smallmoney|  
|**SqlMoney**|smallmoney|  
|十进制 |money|  
|**型**|smalldatetime|  
|**SQLDateTime**|smalldatetime|  
  
## <a name="change-history"></a>更改历史记录  
  
|更新的内容|  
|---------------------|  
|向映射表中添加了**SqlGeography**、 **SqlGeometry**和**SqlHierarchyId**类型。|  
  
## <a name="see-also"></a>另请参阅  
 [.NET Framework 中的 SQL Server 数据类型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
