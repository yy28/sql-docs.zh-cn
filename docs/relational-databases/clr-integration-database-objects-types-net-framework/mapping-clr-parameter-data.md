---
title: 映射 CLR 参数数据 |微软文档
description: 本文列出了 Microsoft SQL Server 数据类型、SQL Server 的 CLR 中的等效项以及 .NET 框架中的本机 CLR 等效项。
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
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488448"
---
# <a name="mapping-clr-parameter-data"></a>映射 CLR 参数数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  下表[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]列出了数据类型、在**System.Data.SqlType**命名空间[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中用于通用语言运行时 （CLR） 中的等效项及其本机 CLR 等效项。  
  
||||  
|-|-|-|  
|**SQL 服务器数据类型**|类型（在 System.Data.SqlTypes 或 Microsoft.SqlServer.Types 中）|**CLR 数据类型 (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64， 空\<无因64>**|  
|**binary**|**SqlBytes, SqlBinary**|**字节***|  
|**bit**|**SqlBoolean**|**布尔、可\<空布尔>**|  
|**char**|无|无|  
|**cursor**|无|无|  
|**date**|**SqlDatetime**|**日期时间，空\<日期时间>**|  
|**datetime**|**SqlDatetime**|**日期时间，空\<日期时间>**|  
|**datetime2**|无|**日期时间，空\<日期时间>**|  
|**日期时间偏移**|**无**|**日期时间偏移，空\<日期时间偏移>**|  
|**decimal**|**SqlDecimal**|**十进制，空\<小数>**|  
|**float**|**SqlDouble**|**双、空\<双>**|  
|**地理**|**SqlGeography**<br /><br /> **Sql地理在**Microsoft.SqlServer.Type.dll 中定义，它与 SQL Server 一起安装，[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]可以从[功能包](https://www.microsoft.com/download/details.aspx?id=52676)下载。|无|  
|**几何**|**SqlGeometry**<br /><br /> **SqlGeometry**在 Microsoft.SqlServer.Type.dll 中定义，它与 SQL Server 一起安装[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，可以从[功能包](https://www.microsoft.com/download/details.aspx?id=52676)下载。|无|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId**在 Microsoft.SqlServer.Type.dll 中定义，该服务器与 SQL Server 一起[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]安装，可以从[功能包](https://www.microsoft.com/download/details.aspx?id=52676)下载。|无|  
|**图像**|无|无|  
|**int**|**SqlInt32**|**Int32， 空\<int32>**|  
|**money**|**SqlMoney**|**十进制，空\<小数>**|  
|**nchar**|**SqlChars， SqlString**|**字符串，字符***|  
|**ntext**|无|无|  
|**numeric**|**SqlDecimal**|**十进制，空\<小数>**|  
|**nvarchar**|**SqlChars， SqlString**<br /><br /> **SQLChars**是数据传输和访问的更好匹配 **，SQLString**更适合执行 String 操作。|**字符串，字符***|  
|**恩瓦尔查尔（1），nchar（1）**|**SqlChars， SqlString**|**字符、字符串、字符、可无字符\<>**|  
|**real**|**SqlSingle（** 但是**SqlSingle**的范围大于**实际**）|**单、空\<单>**|  
|**rowversion**|无|**字节***|  
|**smallint**|**SqlInt16**|**Int16， 空\<无因16>**|  
|**smallmoney**|**SqlMoney**|**十进制，空\<小数>**|  
|**sql_variant**|无|**对象**|  
|**table**|无|无|  
|**text**|无|无|  
|**time**|无|**时间跨度，空\<时间跨度>**|  
|**timestamp**|无|无|  
|**tinyint**|**SqlByte**|**字节，空\<字节>**|  
|**uniqueidentifier**|**SqlGuid**|**吉德， 空可\<贵>**|  
|**用户定义类型（UDT）**|无|绑定到相同程序集或依赖程序集中的用户定义类型的相同类。|  
|**varbinary**|**SqlBytes, SqlBinary**|**字节***|  
|**二进制（1），二进制（1）**|**SqlBytes, SqlBinary**|**字节、字节*、空字节\<>**|  
|**varchar**|无|无|  
|**xml**|**SqlXml**|无|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>使用 Out 参数的自动数据类型转换  
 如果输入参数在**系统中**为 CLR 数据类型，并且调用程序指定其等效数据类型为输入参数，则使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**out**修改器（Microsoft Visual C#） 或**\<out（）> ByRef（）> ByRef（））** 将信息返回调用代码或程序，并且调用程序指定其等效数据类型为输入参数，则当 CLR 方法返回数据类型时，将自动发生类型转换。  
  
 例如，以下 CLR 存储过程具有**SqlInt32** CLR 数据类型的输入参数，该输入参数标有**out** （C#） 或**\<out（）> ByRef（** 可视基本）：  
  
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
  
 在数据库中生成和创建程序集后，使用以下 Transact-SQL 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中创建存储过程，该 SQL 将[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **int**的数据类型指定为 OUTPUT 参数：  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 调用 CLR 存储过程时 **，SqlInt32**数据类型将自动转换为**int**数据类型，并返回到调用程序。  
  
 但是，并非所有 CLR 数据类型都可以通过 out 参数自动转换到其等效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。 下表列出了这些例外类型。  
  
|||  
|-|-|  
|**CLR 数据类型 (SQL Server)**|**SQL 服务器数据类型**|  
|**小数**|smallmoney|  
|**SqlMoney**|smallmoney|  
|**小数**|money|  
|**DateTime**|smalldatetime|  
|**SQLDatetime**|smalldatetime|  
  
## <a name="change-history"></a>更改历史记录  
  
|更新的内容|  
|---------------------|  
|在映射表中添加了**Sql地理学****、SqlGeometry**和**SqlHierarchyId**类型。|  
  
## <a name="see-also"></a>另请参阅  
 [.NET Framework 中的 SQL Server 数据类型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
