---
title: 在应用程序中使用 XML 数据 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- parameters [XML in SQL Server]
- XML [SQL Server], ADO
- columns [XML in SQL Server], ADO.NET
- ADO [XML in SQL Server]
- columns [XML in SQL Server], SQL Server Native Client
- xml data type [SQL Server], ADO
- SQLNCLI, XML
- xml data type [SQL Server], SQL Server Native Client
- SQL Server Native Client, XML
- ADO.NET [XML in SQL Server]
- XML [SQL Server], ADO.NET
- columns [XML in SQL Server], ADO
- xml data type [SQL Server], ADO.NET
- XML [SQL Server], SQL Server Native Client
ms.assetid: 5dabf7e0-c6df-451d-a070-4661f84607fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4d9d64edf29d1e494d25474845295c505caedee8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63232436"
---
# <a name="use-xml-data-in-applications"></a>使用 XML 数据应用程序
  本主题介绍在应用程序中使用 `xml` 数据类型时可用的选项。 本主题包括有关下列操作的信息：  
  
-   使用 ADO 和 `xml` Native Client 处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型列中的 XML  
  
-   使用 ADO.NET 处理 `xml` 类型列中的 XML  
  
-   使用 ADO.NET 处理参数中的 `xml` 类型  
  
## <a name="handling-xml-from-an-xml-type-column-by-using-ado-and-sql-server-native-client"></a>使用 ADO 和 SQL Server Native Client 处理 xml 类型列中的 XML  
 若要使用 MDAC 组件访问 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中引入的类型和功能，必须在 ADO 连接字符串中设置 DataTypeCompatibility 初始化属性。  
  
 例如，下面的 Visual Basic Scripting Edition (VBScript) 示例显示了在 `xml` 示例数据库的 `Demographics` 表中查询 `Sales.Store` 数据类型列 `AdventureWorks2012` 的结果。 具体来讲，查询将为 `CustomerID` 等于 `3`的行查找此列的实例值。  
  
```  
Const DS = "MyServer"  
Const DB = "AdventureWorks2012"  
  
Set objConn = CreateObject("ADODB.Connection")  
Set objRs = CreateObject("ADODB.Recordset")  
  
CommandText = "SELECT Demographics" & _  
              " FROM Sales.Store" & _  
              " INNER JOIN Sales.Customer" & _  
              " ON Sales.Store.BusinessEntityID = sales.customer.StoreID" & _  
              " WHERE Sales.Customer.CustomerID = 3" & _  
              " OR Sales.Customer.CustomerID = 4"  
  
ConnectionString = "Provider=SQLNCLI11" & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;" & _  
                   "DataTypeCompatibility=80"  
  
'Connect to the data source.  
objConn.Open ConnectionString  
  
'Execute command through the connection and display  
Set objRs = objConn.Execute(CommandText)  
  
Dim rowcount  
rowcount = 0  
Do While Not objRs.EOF  
   rowcount = rowcount + 1  
   MsgBox "Row " & rowcount & _  
           vbCrLf & vbCrLf & objRs(0)  
   objRs.MoveNext  
Loop  
  
'Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
```  
  
 此示例显示了如何设置数据类型兼容性属性。 默认情况下，使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 时它设置为 0。 如果将该值设置为 80，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 访问接口将使 `xml` 和用户定义类型列显示为 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 数据类型。 结果将分别是 DBTYPE_WSTR 和 DBTYPE_BYTES。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]还必须在客户端计算机上安装 Native Client，并且连接字符串必须将其指定为用作带有 "`Provider=SQLNCLI11;...`" 的数据提供程序。  
  
#### <a name="to-test-this-example"></a>测试此示例  
  
1.  验证客户端计算机上是否安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 以及是否有 MDAC 2.6.0 或更高版本可用。  
  
     有关详细信息，请参阅 [SQL Server Native Client 编程](../native-client/sql-server-native-client-programming.md)。  
  
2.  确定安装了 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 示例数据库。  
  
     此示例需要 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 示例数据库。  
  
3.  将本主题前面显示的代码复制并粘贴到文本编辑器或代码编辑器中。 将文件另存为 HandlingXmlDataType.vbs。  
  
4.  根据 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装的需要修改脚本并保存更改。  
  
     例如，如果指定了 `MyServer` ，应将其替换为 `(local)` 或安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的服务器的实际名称。  
  
5.  运行 HandlingXmlDataType.vbs 并执行脚本。  
  
 结果应与以下示例输出相似：  
  
```  
Row 1  
  
<StoreSurvey xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>1500000</AnnualSales>  
  <AnnualRevenue>150000</AnnualRevenue>  
  <BankName>Primary International</BankName>  
  <BusinessType>OS</BusinessType>  
  <YearOpened>1974</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>38000</SquareFeet>  
  <Brands>3</Brands>  
  <Internet>DSL</Internet>  
  <NumberEmployees>40</NumberEmployees>  
</StoreSurvey>  
  
Row 2  
  
<StoreSurvey xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>300000</AnnualSales>  
  <AnnualRevenue>30000</AnnualRevenue>  
  <BankName>United Security</BankName>  
  <BusinessType>BM</BusinessType>  
  <YearOpened>1976</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>6000</SquareFeet>  
  <Brands>2</Brands>  
  <Internet>DSL</Internet>  
  <NumberEmployees>5</NumberEmployees>  
</StoreSurvey>  
```  
  
## <a name="handling-xml-from-an-xml-type-column-by-using-adonet"></a>使用 ADO.NET 处理 xml 类型列中的 XML  
 若要使用 ADO.NET 和`xml`来处理数据类型列中的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] XML，可以使用`SqlCommand`类的标准行为。 例如，可以按照使用 `xml` 检索任何 SQL 列的相同方法检索 `SqlDataReader` 数据类型列及其值。但是，如果要将 `xml` 数据类型列的内容作为 XML 使用，必须先将这些内容指派给 `XmlReader` 类型。  
  
 有关详细信息和示例代码，请参阅[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] SDK 文档中的 "数据读取器中的 XML 列值"。  
  
## <a name="handling-an-xml-type-column-in-parameters-by-using-adonet"></a>使用 ADO.NET 处理参数中的 xml 类型列  
 若要处理 ADO.NET 和 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 中作为参数传递的 xml 数据类型，可以将参数值作为 `SqlXml` 数据类型的实例来提供。 这里不涉及任何特殊的处理，因为 `xml` 中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型列可按照与其他列和数据类型（如 `string` 或 `integer`）相同的方式接受参数值。  
  
 有关详细信息和示例代码，请参阅 SDK 文档中的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] "作为命令参数的 XML 值"。  
  
## <a name="see-also"></a>另请参阅  
 [XML 数据 (SQL Server)](xml-data-sql-server.md)  
  
  
