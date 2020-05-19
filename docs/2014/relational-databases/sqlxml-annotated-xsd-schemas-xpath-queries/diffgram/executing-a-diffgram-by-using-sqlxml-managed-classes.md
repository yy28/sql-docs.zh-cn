---
title: 使用 SQLXML 托管类执行 DiffGram |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], Managed Classes
- SQLXML Managed Classes, DiffGrams
- Managed Classes [SQLXML], DiffGrams
- SQLXML, Managed Classes
ms.assetid: 81c687ca-8c9f-4f58-801f-8dabcc508a06
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b0f84dae66bee63d1e7646a6b4e7018d4f071390
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703184"
---
# <a name="executing-a-diffgram-by-using-sqlxml-managed-classes"></a>使用 SQLXML 托管类执行 DiffGram
  此示例演示如何 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用 SQLXML 托管类（node.js）在 .NET Framework 环境中执行 DiffGram 文件，以将数据更新应用到表。  
  
 在本示例中，DiffGram 更新客户 ALFKI 的客户信息（CompanyName 和 ContactName）。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer1"   
                msdata:rowOrder="0" diffgr:hasChanges="modified"   
                CustomerID="ALFKI">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Antonio Moreno</ContactName>  
      </Customer>  
    </DataInstance>  
    <diffgr:before>  
     <Customer diffgr:id="Customer1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
    </diffgr:before>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 ** \< Before>** 块包含** \< Customer>** 元素（**diffgr： id = "Customer1"**）。 ** \< DataInstance>** 块包含具有相同**id**的相应** \< Customer>** 元素。** \< NewDataSet>** 中的** \< customer>** 元素还指定了**diffgr： hasChanges = "modified"**。 这指示一个更新操作，而且 Cust 表中的客户记录也会相应地更新。 请注意，如果未指定**diffgr： hasChanges**属性，DiffGram 处理逻辑将忽略此元素，并且不执行任何更新。  
  
 下面是 c # 教程应用程序的代码，该应用程序演示如何使用 SQLXML 托管类来执行上述 DiffGram，并更新两个表（用户、Ord），你还将在**tempdb**数据库中创建该应用程序。  
  
```  
using System;  
using System.Data;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=MyServer;database=tempdb;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      SqlXmlAdapter ad;  
      // Need a memory stream to hold diff gram temporarily  
      MemoryStream ms = new MemoryStream();  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.RootTag = "ROOT";  
      cmd.CommandStream = new FileStream("MyDiffgram.xml", FileMode.Open, FileAccess.Read);  
      cmd.CommandType = SqlXmlCommandType.DiffGram;  
      cmd.SchemaPath = "DiffGramSchema.xml";  
      // Load data set  
      DataSet ds = new DataSet();  
      ad = new SqlXmlAdapter(cmd);  
      ad.Fill(ds);  
      ad.Update(ds);  
      return 0;  
   }  
   public static int Main(String[] args)  
   {  
      testParams();  
      return 0;  
   }  
}  
```  
  
### <a name="to-test-the-application"></a>测试应用程序  
  
1.  确保已在计算机上安装了 .NET Framework。  
  
2.  将以下 XSD 架构 (DiffGramSchema.xml) 保存在某个文件夹中：  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
     <xsd:annotation>  
      <xsd:documentation>  
        Diffgram Customers/Orders Schema.  
      </xsd:documentation>  
      <xsd:appinfo>  
           <sql:relationship name="CustomersOrders"   
                      parent="Cust"  
                      parent-key="CustomerID"  
                      child-key="CustomerID"  
                      child="Ord"/>  
      </xsd:appinfo>  
     </xsd:annotation>  
     <xsd:element name="Customer" sql:relation="Cust">  
      <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="CompanyName"    type="xsd:string"/>  
          <xsd:element name="ContactName"    type="xsd:string"/>  
           <xsd:element name="Order" sql:relation="Ord" sql:relationship="CustomersOrders">  
            <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:int" sql:field="OrderID"/>  
              <xsd:attribute name="CustomerID" type="xsd:string"/>  
            </xsd:complexType>  
          </xsd:element>  
        </xsd:sequence>  
        <xsd:attribute name="CustomerID" type="xsd:string" sql:field="CustomerID"/>  
      </xsd:complexType>  
     </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  在**tempdb**数据库中创建这些表。  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
4.  添加以下示例数据：  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquer??a', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
5.  复制上面的 DiffGram，并将它粘贴到文本文件中。 在与步骤 1 中所使用文件夹相同的文件夹中将文件另存为 MyDiffGram.xml。  
  
6.  将上面提供的 C# 代码 (DiffgramSample.cs) 保存到先前步骤中用于保存 DiffGramSchema.xml 和 MyDiffGram.xml 的文件夹中。  
  
    > [!NOTE]  
    >  您需要将连接字符串中 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称从“`MyServer`”更新为所安装 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的实际名称。  
  
     如果将该文件存储在不同文件夹中，则必须编辑代码，为映射架构指定相应的目录路径。  
  
7.  编译代码。 若要在命令提示符下编译此代码，请使用：  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DiffgramSample.cs  
    ```  
  
     这将创建一个可执行文件 (DiffgramSample.exe)。  
  
8.  在命令提示符下，执行 DiffgramSample.exe。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SQLXML 4.0&#41;的 DiffGram 示例](diffgram-examples-sqlxml-4-0.md)  
  
  
