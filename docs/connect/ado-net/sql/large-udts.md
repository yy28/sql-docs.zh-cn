---
title: 大型 UDT
description: 演示如何从 SQL Server 2008 中引入的大值 Udt 检索数据。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 420ae24e-762b-4e09-b4c3-2112c470ee49
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 4ea2c0002ceb01606cdf51f04246abcdc74429e0
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452152"
---
# <a name="large-udts"></a>大型 UDT

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

用户定义类型 (UDT) 使开发人员可以通过在 SQL Server 数据库中存储公共语言运行时 (CLR) 对象来扩展服务器的标量类型系统。 UDT 可以包含多个元素，也可以具有多种行为，不同于传统的由单个 SQL Server 系统数据类型组成的别名数据类型。  
  
以前 UDT 的最大大小限制为 8 KB。 在 SQL Server 2008 中，对于 <xref:Microsoft.Data.SqlClient.Server.Format.UserDefined> 格式的 UDT，已不再进行此限制。  
  
有关用户定义类型的完整文档，请参阅 SQL Server 联机丛书中的[CLR 用户定义类型](https://go.microsoft.com/fwlink/?LinkId=98366)。
  
## <a name="retrieving-udt-schemas-using-getschema"></a>使用 GetSchema 检索 UDT 架构  
@No__t_1 的 <xref:Microsoft.Data.SqlClient.SqlConnection.GetSchema%2A> 方法返回 <xref:System.Data.DataTable> 中的数据库架构信息。
  
### <a name="getschematable-column-values-for-udts"></a>Udt 的 GetSchemaTable 列值  
@No__t_1 的 <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A> 方法返回描述列元数据的 <xref:System.Data.DataTable>。 下表描述了 SQL Server 2005 和 SQL Server 2008 之间的大型 Udt 的列元数据之间的差异。  
  
|SqlDataReader 列|SQL Server 2005|SQL Server 2008 和更高版本|  
|--------------------------|---------------------|-------------------------------|  
|`ColumnSize`|不定|不定|  
|`NumericPrecision`|255|255|  
|`NumericScale`|255|255|  
|`DataType`|`Byte[]`|UDT 实例|  
|`ProviderSpecificDataType`|`SqlTypes.SqlBinary`|UDT 实例|  
|`ProviderType`|21 (`SqlDbType.VarBinary`)|29 (`SqlDbType.Udt`)|  
|`NonVersionedProviderType`|29 (`SqlDbType.Udt`)|29 (`SqlDbType.Udt`)|  
|`DataTypeName`|`SqlDbType.VarBinary`|以 Database.SchemaName.TypeName 形式指定的由三部分组成的名称  。|  
|`IsLong`|不定|不定|  
  
## <a name="sqldatareader-considerations"></a>SqlDataReader 注意事项  
<xref:Microsoft.Data.SqlClient.SqlDataReader> 在 SQL Server 2008 中已得到扩展，可支持检索大型 UDT 值。 @No__t_0 处理大的 UDT 值的方式取决于所使用 SQL Server 的版本，以及连接字符串中指定的 `Type System Version`。 有关详细信息，请参阅 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>为止。  
  
当 `Type System Version` 设置为 SQL Server 2005 时，以下 <xref:Microsoft.Data.SqlClient.SqlDataReader> 方法将返回 <xref:System.Data.SqlTypes.SqlBinary> 而不是 UDT：  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>  
  
当 `Type System Version` 设置为 SQL Server 2005 时，以下方法将返回 `Byte[]` 的数组，而不是 UDT：  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>  
  
- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>  
  
注意，未对当前版本的 ADO.NET 执行转换。  
  
## <a name="specifying-sqlparameters"></a>指定 SqlParameters  
以下 <xref:Microsoft.Data.SqlClient.SqlParameter> 属性已扩展为适用于大型 Udt。  
  
|SqlParameter 属性|描述|  
|---------------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|获取或设置一个对象，该对象表示参数的值。 默认值为 NULL。 此属性可以是 `SqlBinary`、`Byte[]` 或托管对象。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|获取或设置一个对象，该对象表示参数的值。 默认值为 NULL。 此属性可以是 `SqlBinary`、`Byte[]` 或托管对象。|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|获取或设置要解析的参数值的大小。 默认值为 0。 此属性可以是一个表示参数值大小的整数。 对于大型 UDT，此属性可以是 UDT 的实际大小，也可以是 -1，表示未知。|  
  
## <a name="retrieving-data-example"></a>检索数据示例  
下面的代码段演示如何检索大型 UDT 数据。 @No__t_0 变量假定连接到 SQL Server 数据库，而 `commandString` 变量假定有效的 SELECT 语句中首先列出主键列。  
  
```csharp  
using (SqlConnection connection = new SqlConnection(   
    connectionString, commandString))  
{  
  connection.Open();  
  SqlCommand command = new SqlCommand(commandString);  
  SqlDataReader reader = command.ExecuteReader();  
  while (reader.Read())  
  {  
    // Retrieve the value of the Primary Key column.  
    int id = reader.GetInt32(0);  
  
    // Retrieve the value of the UDT.  
    LargeUDT udt = (LargeUDT)reader[1];  
  
    // You can also use GetSqlValue and GetValue.  
    // LargeUDT udt = (LargeUDT)reader.GetSqlValue(1);  
    // LargeUDT udt = (LargeUDT)reader.GetValue(1);  
  
    Console.WriteLine(  
     "ID={0} LargeUDT={1}", id, udt);  
  }  
reader.close  
}  
```  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 二进制和大值数据](sql-server-binary-large-value-data.md)
