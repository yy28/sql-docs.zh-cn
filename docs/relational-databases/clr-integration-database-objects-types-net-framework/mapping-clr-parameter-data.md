---
title: "将 CLR 参数数据映射 |Microsoft 文档"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
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
caps.latest.revision: "71"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: bee49e277d3492dc93bcdf29b65c1c3007cebe50
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="mapping-clr-parameter-data"></a>映射 CLR 参数数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]下表列出[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型，公共语言运行时 (CLR) 来中的等效项[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中**System.Data.SqlTypes**命名空间，和中的本机 CLR 等效项[!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET framework。  
  
||||  
|-|-|-|  
|**SQL Server 数据类型**|类型（在 System.Data.SqlTypes 或 Microsoft.SqlServer.Types 中）|**CLR 数据类型 (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64，可以为 Null\<Int64 >**|  
|**binary**|**对 SqlBinary**|**Byte]**|  
|**bit**|**SqlBoolean**|**布尔值、 可以为 Null\<布尔 >**|  
|**char**|无|无|  
|**cursor**|无|无|  
|**date**|**SqlDateTime**|**日期/时间，可以为 Null\<DateTime >**|  
|**datetime**|**SqlDateTime**|**日期/时间，可以为 Null\<DateTime >**|  
|**datetime2**|无|**日期/时间，可以为 Null\<DateTime >**|  
|**DATETIMEOFFSET**|**无**|**DateTimeOffset，可以为 Null\<DateTimeOffset >**|  
|**decimal**|**SqlDecimal**|**Decimal、 可以为 Null\<十进制 >**|  
|**float**|**SqlDouble**|**双精度，可以为 Null\<Double >**|  
|**地理**|**SqlGeography**<br /><br /> **SqlGeography**中 Microsoft.SqlServer.Types.dll 与 SQL Server 安装，并且可以从下载定义[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][功能包](https://www.microsoft.com/download/details.aspx?id=52676)。|无|  
|**geometry**|**SqlGeometry**<br /><br /> **SqlGeometry**中 Microsoft.SqlServer.Types.dll 与 SQL Server 安装，并且可以从下载定义[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][功能包](https://www.microsoft.com/download/details.aspx?id=52676)。|无|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId**中 Microsoft.SqlServer.Types.dll 与 SQL Server 安装，并且可以从下载定义[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][功能包](https://www.microsoft.com/download/details.aspx?id=52676)。|无|  
|**image**|无|无|  
|**int**|**SqlInt32**|**Int32，可以为 Null\<Int32 >**|  
|**money**|**SqlMoney**|**Decimal、 可以为 Null\<十进制 >**|  
|**nchar**|**对 SqlString**|**字符串，Char]**|  
|**ntext**|无|无|  
|**numeric**|**SqlDecimal**|**Decimal、 可以为 Null\<十进制 >**|  
|**nvarchar**|**对 SqlString**<br /><br /> **对**数据传输和访问权限，更好的匹配和**SQLString**是执行字符串操作的更好的匹配项。|**字符串，Char]**|  
|**nvarchar(1)、 nchar(1)**|**对 SqlString**|**Char、 字符串，Char []，可以为 Null\<char >**|  
|**real**|**以**(的范围**以**，但是，大于**实际**)|**单个，为 Null\<单个 >**|  
|**rowversion**|无|**Byte]**|  
|**int**|**SqlInt16**|**Int16，可以为 Null\<Int16 >**|  
|**smallmoney**|**SqlMoney**|**Decimal、 可以为 Null\<十进制 >**|  
|**sql_variant**|无|**对象**|  
|**table**|无|无|  
|**text**|无|无|  
|**time**|无|**时间跨度，可以为 Null\<TimeSpan >**|  
|**timestamp**|无|无|  
|**tinyint**|**以**|**字节，可以为 Null\<字节 >**|  
|**uniqueidentifier**|**SqlGuid**|**Guid，可以为 Null\<Guid >**|  
|**用户定义 type(UDT)**|无|绑定到相同程序集或依赖程序集中的用户定义类型的相同类。|  
|**varbinary**|**对 SqlBinary**|**Byte]**|  
|**varbinary(1)、 binary(1)**|**对 SqlBinary**|**字节、 Byte []，可以为 Null\<字节 >**|  
|**varchar**|无|无|  
|**xml**|**SqlXml**|无|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>使用 Out 参数的自动数据类型转换  
 CLR 方法可通过将标记与输入的参数与调用的代码或程序返回信息**出**修饰符 (Microsoft Visual C#) 或 **\<out （) > ByRef** (Microsoft Visual Basic)如果输入的参数是中的 CLR 数据类型**System.Data.SqlTypes**命名空间，并且调用程序指定它的等效项[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型作为输入参数，会自动发生类型转换如果 CLR 方法返回的数据类型。  
  
 例如，以下 CLR 存储过程具有输入的参数的**SqlInt32** CLR 数据类型将标有**出**(C#) 或 **\<out （) > ByRef** (Visual Basic):  
  
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
  
 构建并在数据库中创建程序集后，在中创建存储的过程[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用以下 TRANSACT-SQL，它指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型的**int**作为输出参数：  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 当 CLR 存储过程被调用**SqlInt32**数据类型自动转换为**int**数据类型，并返回到调用程序。  
  
 但是，并非所有 CLR 数据类型都可以通过 out 参数自动转换到其等效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。 下表列出了这些例外类型。  
  
|||  
|-|-|  
|**CLR 数据类型 (SQL Server)**|**SQL Server 数据类型**|  
|**十进制**|smallmoney|  
|**SqlMoney**|smallmoney|  
|**十进制**|money|  
|**DateTime**|smalldatetime|  
|**SQLDateTime**|smalldatetime|  
  
## <a name="change-history"></a>更改历史记录  
  
|更新内容|  
|---------------------|  
|添加**SqlGeography**， **SqlGeometry**，和**SqlHierarchyId**到映射表的类型。|  
  
## <a name="see-also"></a>另请参阅  
 [.NET Framework 中的 SQL Server 数据类型](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
