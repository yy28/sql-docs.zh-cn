---
title: 使用 ADO 和 OLE DB 驱动程序一起用于 SQL Server |Microsoft 文档
description: 使用 ADO 和 OLE DB 驱动程序一起用于 SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, ADO
- data access [OLE DB Driver for SQL Server], ADO
- ADO [OLE DB Driver for SQL Server]
- MSOLEDBSQL, ADO
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b4888cc0054a8cf3c22b49aa28baf2c23577a48d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="using-ado-with-ole-db-driver-for-sql-server"></a>使用 ADO 和 OLE DB 驱动程序一起用于 SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  若要在中引入的新功能利用[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]如多个活动结果集 (MARS)、 查询通知、 用户定义类型 (Udt)，或新**xml**数据类型，使用 ActiveX 现有应用程序数据对象 (ADO) 应使用 OLE DB 驱动程序适用于 SQL Server 作为其数据访问接口。  
  
 若要启用要使用的最新版本的新功能的 ADO [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，一些增强功能进行了 OLE DB 驱动程序的 SQL Server 扩展了 OLE DB 的核心功能。 这些增强功能允许 ADO 应用程序使用较新[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]功能以及使用两个数据类型中引入[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]: **xml**和**udt**。 这些增强功能还利用增强功能**varchar**， **nvarchar**，和**varbinary**数据类型。 OLE DB 驱动程序的 SQL Server 将 SSPROP_INIT_DATATYPECOMPATIBILITY 初始化属性添加到 dbpropset_sqlserverdbinit 限设置的属性使用 ADO 应用程序，因此新的数据类型公开与 ADO 兼容的方式。 此外，SQL Server 的 OLE DB 驱动程序还定义一个新的名为的连接字符串关键字**DataTypeCompatibility** ，设置连接字符串中。  

> [!NOTE]  
>  现有 ADO 应用程序可以使用 SQLOLEDB 访问接口来访问和更新 XML、UDT 以及大型值文本和二进制字段值。 新更大**varchar （max)**， **nvarchar (max)**，和**varbinary （max)** 数据类型会返回 ADO 类型**adLongVarChar**，**adLongVarWChar**和**adLongVarBinary**分别。 XML 列返回为**adLongVarChar**，并且 UDT 列返回为**感**。 但是，如果使用 OLE DB 驱动程序的 SQL Server (MSOLEDBSQL) 而不是 SQLOLEDB，你需要确保设置**DataTypeCompatibility**为"80"关键字，以便新的数据类型会正确映射到 ADO 数据类型。  

## <a name="enabling-ole-db-driver-for-sql-server-from-ado"></a>启用从 ADO 的 SQL Server 的 OLE DB 驱动程序  
 若要启用 SQL Server 的 OLE DB 驱动程序的使用情况，ADO 应用程序将需要在其连接字符串中实现以下关键字：  

-   `Provider=MSOLEDBSQL`  

-   `DataTypeCompatibility=80`  

 有关 ADO 连接字符串关键字在 OLE DB 驱动程序中受支持的 SQL Server，请参阅[OLE DB 驱动程序的 SQL Server 连接字符串关键字](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。  

 下面是建立一个完全启用使其与 OLE DB 驱动程序适用于 SQL Server，包括启用 MARS 功能的 ADO 连接字符串的示例：  

```  
Dim con As New ADODB.Connection  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
```  

## <a name="examples"></a>示例  
 下列各节提供如何使用 ADO 与 OLE DB 驱动程序适用于 SQL Server 的示例。  

### <a name="retrieving-xml-column-data"></a>检索 XML 列数据  
 在此示例中，记录集用于检索和显示中的 XML 列中的数据[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **AdventureWorks**示例数据库。  

```  
Dim con As New ADODB.Connection  
Dim rst As New ADODB.Recordset  
Dim sXMLResult As String  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _   
         & "DataTypeCompatibility=80;"  

con.Open  

' Get the xml data as a recordset.  
Set rst.ActiveConnection = con  
rst.Source = "SELECT AdditionalContactInfo FROM Person.Contact " _  
   & "WHERE AdditionalContactInfo IS NOT NULL"  
rst.Open  

' Display the data in the recordset.  
While (Not rst.EOF)  
   sXMLResult = rst.Fields("AdditionalContactInfo").Value  
   Debug.Print (sXMLResult)  
   rst.MoveNext  
End While  

con.Close  
Set con = Nothing  
```  

> [!NOTE]  
>  XML 列不支持记录集筛选。 如果使用，将返回错误。  

### <a name="retrieving-udt-column-data"></a>检索 UDT 列数据  
 在此示例中，**命令**对象用于执行 SQL 查询返回 UDT 更新 UDT 数据时，，然后将新的数据插入回数据库。 此示例假定**点**UDT 已注册数据库中。  

```  
Dim con As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
Dim strOldUDT As String  
Dim strNewUDT As String  
Dim aryTempUDT() As String  
Dim strTempID As String  
Dim i As Integer  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;"  

con.Open  

' Get the UDT value.  
Set cmd.ActiveConnection = con  
cmd.CommandText = "SELECT ID, Pnt FROM dbo.Points.ToString()"  
Set rst = cmd.Execute  
strTempID = rst.Fields(0).Value  
strOldUDT = rst.Fields(1).Value  

' Do something with the UDT by adding i to each point.  
arytempUDT = Split(strOldUDT, ",")  
i = 3  
strNewUDT = LTrim(Str(Int(aryTempUDT(0)) + i)) + "," + _  
   LTrim(Str(Int(aryTempUDT(1)) + i))  

' Insert the new value back into the database.  
cmd.CommandText = "UPDATE dbo.Points SET Pnt = '" + strNewUDT + _  
   "' WHERE ID = '" + strTempID + "'"  
cmd.Execute  

con.Close  
Set con = Nothing  
```  

### <a name="enabling-and-using-mars"></a>启用和使用 MARS  
 在此示例中，连接字符串构造以启用 MARS 通过 OLE DB 驱动程序的 SQL Server，然后创建两个记录集对象以执行使用相同的连接。  

```  
Dim con As New ADODB.Connection  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  

Dim recordset1 As New ADODB.Recordset  
Dim recordset2 As New ADODB.Recordset  

Dim recordsaffected As Integer  
Set recordset1 =  con.Execute("SELECT * FROM Table1", recordsaffected, adCmdText)  
Set recordset2 =  con.Execute("SELECT * FROM Table2", recordsaffected, adCmdText)  

con.Close  
Set con = Nothing  
```  

 在以前的 OLE DB 访问接口版本中，该代码会导致在第二次执行时创建隐式的连接，因为每个单独的连接只能打开一个活动的结果集。 由于该隐式连接未加入 OLE DB 连接池，因此这会导致额外的开销。 使用 SQL Server 的 OLE DB 驱动程序由公开 MARS 功能，一个连接上获取多个活动的结果。  

## <a name="see-also"></a>另请参阅  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
