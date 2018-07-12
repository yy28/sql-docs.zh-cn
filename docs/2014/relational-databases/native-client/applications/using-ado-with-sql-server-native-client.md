---
title: 用于 SQL Server Native Client 使用 ADO |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client  - "database-engine" - "docset-sql-devref"
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, ADO
- data access [SQL Server Native Client], ADO
- ADO [SQL Server Native Client]
- SQLNCLI, ADO
ms.assetid: 118a7cac-4c0d-44fd-b63e-3d542932d239
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62c8430e36fe0982d4dc8e9ec56e14d124ccd106
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37431816"
---
# <a name="using-ado-with-sql-server-native-client"></a>将 ADO 用于 SQL Server Native Client
  若要充分利用新功能中引入[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]如多个活动结果集 (MARS)、 查询通知、 用户定义类型 (Udt) 或新**xml**数据类型，使用 ActiveX 的现有应用程序数据对象 (ADO) 应使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序作为其数据访问接口。  
  
 如果不需要使用在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中引入的任何新功能，则不需要使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口；您可以继续使用当前数据访问接口（通常是 SQLOLEDB）。 如果要增强现有应用程序的功能，并且需要使用在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中引入的新功能，则应当使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口。  
  
> [!NOTE]  
>  如果要开发新的应用程序，则建议考虑使用用于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的 ADO.NET 和 .NET Framework 数据访问接口，而不是使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client，以访问最新 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本的所有新功能。 有关用于 .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的详细信息，请参阅针对 ADO.NET 的 .NET Framework SDK 文档。  
  
 为了使 ADO 能够使用最新 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本的新功能，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口已进行了某些增强，这些增强扩展了 OLE DB 的核心功能。 这些增强功能允许 ADO 应用程序使用较新[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]功能并使用两个数据类型中引入[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]: **xml**并**udt**。 这些增强功能还可以利用的增强功能**varchar**， **nvarchar**，并**varbinary**数据类型。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 将 SSPROP_INIT_DATATYPECOMPATIBILITY 初始化属性添加到 DBPROPSET_SQLSERVERDBINIT 属性集用于供 ADO 应用程序，以便与 ADO 兼容的方式公开新的数据类型。 此外， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序还定义了名为的新连接字符串关键字`DataTypeCompatibility`，设置连接字符串中。  
  
> [!NOTE]  
>  现有 ADO 应用程序可以使用 SQLOLEDB 访问接口来访问和更新 XML、UDT 以及大型值文本和二进制字段值。 新较大**varchar （max)**， **nvarchar （max)**，并**varbinary （max)** 数据类型将作为 ADO 类型返回**adLongVarChar**，**adLongVarWChar**并**adLongVarBinary**分别。 XML 列返回作为**adLongVarChar**，并作为返回 UDT 列**adVarBinary**。 但是，如果使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口 (SQLNCLI11) 而不是 SQLOLEDB，则需要确保将 `DataTypeCompatibility` 关键字设置为“80”，以便新数据类型能正确映射到 ADO 数据类型。  
  
## <a name="enabling-sql-server-native-client-from-ado"></a>从 ADO 启用 SQL Server Native Client  
 若要启用的使用情况[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client，ADO 应用程序将需要在其连接字符串中实现以下关键字：  
  
-   `Provider=SQLNCLI11`  
  
-   `DataTypeCompatibility=80`  
  
 有关详细信息的 ado 连接字符串中支持的关键字[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client，请参阅[将连接字符串关键字用于 SQL Server Native Client](using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 以下是建立完全启用以便与 ADO 连接字符串的示例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端，包括启用 MARS 功能：  
  
```  
Dim con As New ADODB.Connection  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
```  
  
## <a name="examples"></a>示例  
 以下部分举例说明如何使用 ADO 与[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。  
  
### <a name="retrieving-xml-column-data"></a>检索 XML 列数据  
 在此示例中，记录集用于检索和显示中的 XML 列中的数据[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **AdventureWorks**示例数据库。  
  
```  
Dim con As New ADODB.Connection  
Dim rst As New ADODB.Recordset  
Dim sXMLResult As String  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
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
 在此示例中，**命令**对象用于执行返回 UDT 的 SQL 查询、 更新 UDT 数据时，，然后将新数据插入回数据库。 此示例假定**点**已在数据库中注册 UDT。  
  
```  
Dim con As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
Dim strOldUDT As String  
Dim strNewUDT As String  
Dim aryTempUDT() As String  
Dim strTempID As String  
Dim i As Integer  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
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
 在此示例中，构造连接字符串以启用通过 MARS[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]创建 Native Client OLE DB 提供程序和两个记录集对象以使用同一连接执行。  
  
```  
Dim con As New ADODB.Connection  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
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
  
 在以前的 OLE DB 访问接口版本中，该代码会导致在第二次执行时创建隐式的连接，因为每个单独的连接只能打开一个活动的结果集。 由于该隐式连接未加入 OLE DB 连接池，因此这会导致额外的开销。 使用 MARS 功能公开的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序，您在一个连接上获取多个活动的结果。  
  
## <a name="see-also"></a>请参阅  
 [使用 SQL Server Native Client 生成应用程序](building-applications-with-sql-server-native-client.md)  
  
  
