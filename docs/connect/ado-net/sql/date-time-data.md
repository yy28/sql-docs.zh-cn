---
title: 日期和时间数据
description: 介绍了如何使用 SQL Server 2008 中引入的新日期和时间数据类型。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 75d8b98726a758e0533053dbdf8d2e03b3bfdf0d
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896988"
---
# <a name="date-and-time-data"></a>日期和时间数据

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server 2008 引入了新数据类型，用于处理日期和时间信息。 新数据类型包括独立的日期和时间类型，以及具有更大范围、精度且时区感知的扩展数据类型。 Microsoft SqlClient Data Provider for SQL Server (<xref:Microsoft.Data.SqlClient>) 完全支持 SQL Server 2008 数据库引擎的所有新功能。 必须安装 .NET Framework 3.5 SP1（或更高版本）或 .NET Core 1.0（或更高版本），才能结合使用这些新功能和 SqlClient。  
  
SQL Server 2008 之前的 SQL Server 版本仅具有两种用于处理日期和时间值的数据类型：`datetime` 和 `smalldatetime`。 这两种数据类型都同时包含日期值和时间值，难以仅使用日期值或仅使用时间值。 此外，这些数据类型只支持在 1753 年英国引入公历之后的日期。 另一个限制是，这些旧数据类型无法感知时区，这使得处理来自多个时区的数据变得困难。  
  
SQL Server 联机丛书中有关于 SQL Server 数据类型的完整文档。 有关日期和时间数据的入门级主题，请参阅[使用日期和时间数据](https://go.microsoft.com/fwlink/?LinkID=98361)。
  
## <a name="datetime-data-types-introduced-in-sql-server-2008"></a>SQL Server 2008 中引入的日期/时间数据类型  
 下表介绍了新日期和时间数据类型。  
  
|SQL Server 数据类型|说明|  
|--------------------------|-----------------|  
|`date`|`date` 数据类型的范围从 01 年 1 月 1 日 9999 年 12 月 31 日，精确到 1 天。 默认值为 January 1, 1900。 存储大小为 3 个字节。|  
|`time`|`time` 数据类型仅采用 24 小时制存储时间值。 `time` 数据类型介于 00:00:00.0000000 到 23:59:59.9999999 范围之间，准确度为 100 纳秒。 默认值为 00:00:00.0000000（午夜）。 `time` 数据类型支持用户定义的小数秒精度，存储大小根据指定的精度在 3 字节到 6 字节之间变化。|  
|`datetime2`|`datetime2` 数据类型将 `date` 和 `time` 数据类型的范围和精度合并为一个数据类型。<br /><br /> 默认值和字符串文本格式与 `date` 和 `time` 数据类型中定义的相同。|  
|`datetimeoffset`|`datetimeoffset` 数据类型具有 `datetime2` 的所有功能，并添加了时区偏移量。 时区偏移量表示为 [+&#124;-] HH:MM。 HH 是两位数，介于 00 和 14 范围之间，表示时区偏移量中的小时数。 MM 是两位数，范围为 00 到 59，表示时区偏移量中的额外分钟数。 时间格式支持到 100 毫微秒。 必需符号 + 或 - 指明是在 UTC（协调世界时或格林威治标准时间）中加上还是减去时区偏移来获得本地时间。|  
  
> [!NOTE]
>  要详细了解如何使用 `Type System Version`，请参阅 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>。  
  
## <a name="date-format-and-date-order"></a>日期格式和日期顺序  
SQL Server 如何分析日期和时间值不仅取决于类型系统版本和服务器版本，还取决于服务器的默认语言和格式设置。 如果日期格式使用一种语言，而查询是通过使用不同语言和日期格式设置的连接执行的，那么可能无法识别采用日期格式的日期字符串。  
  
Transact-SQL SET LANGUAGE 语句隐式设置确定日期部分顺序的 DATEFORMAT。 可以通过按 MDY、DMY、YMD、YDM、MYD 或 DYM 顺序对日期部分进行排序，对连接使用 SET DATEFORMAT Transact-SQL 语句来区分日期值。  
  
如果你没有为连接指定任何 DATEFORMAT，SQL Server 会使用与连接关联的默认语言。 例如，为日期字符串“01/02/03”在语言设置为美式英语的服务器上解析为 MDY（2003 年 1 月 2 日），而在语言设置为英式英语的服务器上则解析为 DMY（2003 年 2 月 1 日）。 年份是由 SQL Server 的临界年份规则确定的，此规则定义了用于指定世纪值的临界日期。 有关详细信息，请参阅 SQL Server 联机丛书中的 [two digit year cutoff 选项](https://go.microsoft.com/fwlink/?LinkId=120473)。  
  
> [!NOTE]
>  从字符串格式转换为 `date`、`time`、`datetime2` 或 `datetimeoffset` 时，不支持使用 YDM 日期格式。  
  
要详细了解 SQL Server 如何解释日期和时间数据，请参见 SQL Server 2008 联机丛书中的[使用日期和时间数据](https://go.microsoft.com/fwlink/?LinkID=98361)。  
  
## <a name="datetime-data-types-and-parameters"></a>日期/时间数据类型和参数  
为了支持新日期和时间数据类型，已向 <xref:System.Data.SqlDbType> 中添加了下列枚举。  
  
- `SqlDbType.Date`  
  
- `SqlDbType.Time`  
  
- `SqlDbType.DateTime2`  
  
- `SqlDbType.DateTimeOffSet`  

通过使用 <xref:System.Data.SqlDbType> 枚举之一，可以指定 <xref:Microsoft.Data.SqlClient.SqlParameter> 的数据类型。 

> [!NOTE]
> 无法将 `SqlParameter` 的 `DbType` 属性设置为 `SqlDbType.Date`。

也可以采用通用的方式通过将 `SqlParameter` 对象的 <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> 属性设置为特定的 <xref:System.Data.DbType> 枚举值来指定 <xref:Microsoft.Data.SqlClient.SqlParameter> 的类型。 <xref:System.Data.DbType> 中已添加了下面的枚举值，以支持 `datetime2` 和 `datetimeoffset` 数据类型：  
  
- DbType.DateTime2  
  
- DbType.DateTimeOffset  
  
这些新枚举补充了 `Date`、`Time` 和 `DateTime` 枚举。  
  
参数对象的 Microsoft SqlClient 数据提供程序类型是根据参数对象值的 .NET 类型或参数对象的 `DbType` 推断出来的。 没有引入新 <xref:System.Data.SqlTypes> 数据类型来支持新日期和时间数据类型。 下表介绍了 SQL Server 2008 日期和时间数据类型与 CLR 数据类型之间的映射。  
  
|SQL Server 数据类型|.NET 类型|System.Data.SqlDbType|System.Data.DbType|  
|--------------------------|-------------------------|---------------------------|------------------------|  
|date|System.DateTime|Date|Date|  
|time|System.TimeSpan|时间|时间|  
|datetime2|System.DateTime|DateTime2|DateTime2|  
|datetimeoffset|System.DateTimeOffset|DateTimeOffset|DateTimeOffset|  
|datetime|System.DateTime|DateTime|DateTime|  
|smalldatetime|System.DateTime|DateTime|DateTime|  
  
### <a name="sqlparameter-properties"></a>SqlParameter 属性  
 下表介绍了与日期和时间数据类型相关的 `SqlParameter` 属性。  
  
|properties|说明|  
|--------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.IsNullable%2A>|获取或设置值是否可为空。 将空参数值发送到服务器时，必须指定 <xref:System.DBNull>，而不是 `null`（在 Visual Basic 中为 `Nothing`）。 若要详细了解数据库空值，请参阅[处理空值](handle-null-values.md)。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Precision%2A>|获取或设置用于表示该值的最大位数。 对于日期和时间数据类型，此设置将被忽略。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Scale%2A>|获取或设置要将 `Time`、`DateTime2` 和 `DateTimeOffset` 值的时间部分解析到的小数位数。 默认值为 0；也就是说，实际确定位数是根据值推断出来并发送到服务器的。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|对于日期和时间数据类型，此属性将被忽略。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|获取或设置参数值。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|获取或设置参数值。|  
  
> [!NOTE]
>  小于零或大于等于 24 小时的时间值会导致 <xref:System.ArgumentException> 抛出。  
  
### <a name="creating-parameters"></a>创建参数  
可以创建 <xref:Microsoft.Data.SqlClient.SqlParameter> 对象，具体方法为使用它的构造函数，或将它添加到 <xref:Microsoft.Data.SqlClient.SqlCommand>.<xref:Microsoft.Data.SqlClient.SqlCommand.Parameters%2A> 集合（通过调用 <xref:Microsoft.Data.SqlClient.SqlParameterCollection> 的 `Add` 方法）。 `Add` 方法需要使用构造函数参数或现有参数对象作为输入。  
  
本主题接下来的几个部分举例介绍了如何指定日期和时间参数。
  
### <a name="date-example"></a>日期示例  
下面的代码片段展示了如何指定 `date` 参数。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Date";  
parameter.SqlDbType = SqlDbType.Date;  
parameter.Value = "2007/12/1";  
```  
  
### <a name="time-example"></a>时间示例  
下面的代码片段展示了如何指定 `time` 参数。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@time";  
parameter.SqlDbType = SqlDbType.Time;  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
### <a name="datetime2-example"></a>Datetime2 示例  
下面的代码片段展示了如何指定同时包含日期和时间部分的 `datetime2` 参数。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Datetime2";  
parameter.SqlDbType = SqlDbType.DateTime2;  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
### <a name="datetimeoffset-example"></a>DateTimeOffSet 示例  
下面的代码片段展示了如何指定包含日期、时间和时区偏移 0 的 `DateTimeOffSet` 参数。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@DateTimeOffSet";  
parameter.SqlDbType = SqlDbType.DateTimeOffSet;  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
### <a name="addwithvalue"></a>AddWithValue  
也可以使用 <xref:Microsoft.Data.SqlClient.SqlCommand> 的 `AddWithValue` 方法来提供参数，如下面的代码片段所示。 不过，`AddWithValue` 方法不允许为参数指定 <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> 或 <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A>。  
  
```csharp  
command.Parameters.AddWithValue(   
    "@date", DateTimeOffset.Parse("16660902"));  
```  
  
`@date` 参数可映射到服务器上的 `date`、`datetime` 或 `datetime2` 数据类型。 使用新 `datetime` 数据类型时，必须将参数的 <xref:System.Data.SqlDbType> 属性显式设置为实例的数据类型。 使用 <xref:System.Data.SqlDbType.Variant> 或隐式提供参数值可能会导致与 `datetime` 和 `smalldatetime` 数据类型出现向后兼容性问题。  
  
下表展示了哪些 `SqlDbTypes` 是根据哪些 CLR 类型推断出来的：  
  
|CLR 类型|Inferred SqlDbType|  
|--------------|------------------------|  
|DateTime|SqlDbType.DateTime|  
|TimeSpan|SqlDbType.Time|  
|DateTimeOffset|SqlDbType.DateTimeOffset|  
  
## <a name="retrieving-date-and-time-data"></a>检索日期和时间数据  
下表说明用于检索 SQL Server 2008 日期和时间值的方法。  
  
|SqlClient 方法|说明|  
|----------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTime%2A>|以 <xref:System.DateTime> 结构形式检索指定的列值。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|以 <xref:System.DateTimeOffset> 结构形式检索指定的列值。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>|返回作为字段的基础提供程序专用类型的类型。 对于新日期和时间类型，返回与 `GetFieldType` 相同的类型。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>|获取指定列的值。 对于新日期和时间类型，返回与 `GetValue` 相同的类型。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>|检索指定数组中的值。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlString%2A>|检索列值作为 <xref:System.Data.SqlTypes.SqlString>。 如果数据无法表示为 `SqlString`，则会导致 <xref:System.InvalidCastException> 抛出。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>|检索列数据作为默认 `SqlDbType`。 对于新日期和时间类型，返回与 `GetValue` 相同的类型。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>|检索指定数组中的值。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetString%2A>|如果 Type System Version 设置为 SQL Server 2005，则以字符串形式检索列值。 如果数据无法表示为字符串，则会导致 <xref:System.InvalidCastException> 抛出。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetTimeSpan%2A>|以 <xref:System.TimeSpan> 结构形式检索指定的列值。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>|检索指定列值作为基础 CLR 类型。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>|检索数组中的列值。|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>|返回描述结果集的元数据的 <xref:System.Data.DataTable>。|  
  
> [!NOTE]
>  正在 SQL Server 中执行的代码不支持新日期和时间 `SqlDbTypes`。 如果将其中一种类型传递给服务器，则会导致异常抛出。  
  
## <a name="specifying-date-and-time-values-as-literals"></a>将日期和时间值指定为文本  
可以使用各种不同的文本字符串格式来指定日期和时间数据类型，随后 SQL Server 在运行时进行评估，并将它们转换为内部日期/时间结构。 SQL Server 识别用单引号 (') 括起来的日期和时间数据。 下面的示例展示了一些格式：  
  
- 字母日期格式，如 `'October 15, 2006'`。  
  
- 数字日期格式，如 `'10/15/2006'`。  
  
- 如果使用的是 ISO 标准日期格式，未分隔的字符串格式 `'20061015'`（举个例子）就会解析为 2006 年 10 月 15 日。  
  
> [!NOTE]
>  SQL Server 联机丛书中有关于所有文本字符串格式以及日期和时间数据类型的其他功能的完整文档。  
  
小于零或大于等于 24 小时的时间值会导致 <xref:System.ArgumentException> 抛出。  
  
## <a name="resources-in-sql-server-2008-books-online"></a>SQL Server 2008 联机丛书中的资源  
若要详细了解如何在 SQL Server 2008 中处理日期和时间值，请参阅 SQL Server 2008 联机丛书中的以下资源。  
  
|主题|说明|  
|-----------|-----------------|  
|[日期和时间数据类型及函数 (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=98360)|概述所有 Transact-SQL 日期和时间数据类型和函数。|  
|[使用日期和时间数据](https://go.microsoft.com/fwlink/?LinkId=98361)|提供日期和时间数据类型和函数的相关信息以及使用示例。|  
|[数据类型 (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=98362)|介绍了 SQL Server 2008 中的系统数据类型。|  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 数据类型和 ADO.NET](sql-server-data-types.md)
