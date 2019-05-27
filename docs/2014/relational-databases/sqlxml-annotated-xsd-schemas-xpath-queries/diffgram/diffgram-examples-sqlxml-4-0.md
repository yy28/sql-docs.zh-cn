---
title: DiffGram 示例 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], examples
- examples [SQLXML], DiffGram
- diffgr:parentID
- parentID annotation
ms.assetid: fc148583-dfd3-4efb-a413-f47b150b0975
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 38bee43ed5b727bca552c1b44010dd692012d823
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66012964"
---
# <a name="diffgram-examples-sqlxml-40"></a>DiffGram 示例 (SQLXML 4.0)
  本主题中的示例包括用于对数据库执行插入、更新和删除操作的多个 DiffGram。 在使用这些示例前，请注意以下事项：  
  
-   示例中使用两个表（Cust 和 Ord）；要测试 DiffGram 示例，必须创建这两个表：  
  
    ```  
    Cust(CustomerID, CompanyName, ContactName)  
    Ord(OrderID, CustomerID)  
    ```  
  
-   本主题中的多数示例都使用以下 XSD 架构：  
  
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
  
     将此架构另存为 DiffGramSchema.xml，并与示例中所用的其他文件保存在相同的文件夹中。  
  
## <a name="a-deleting-a-record-by-using-a-diffgram"></a>A. 使用 DiffGram 删除记录  
 本示例中的 DiffGram 从 Cust 表中删除一条客户记录（CustomerID 为 ALFKI），并且从 Ord 表中删除相应的订单记录（OrderID 为 1）。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance/>  
  
    <diffgr:before>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI"   
               OrderID="1"/>  
        <Customer diffgr:id="Customer1"   
                  msdata:rowOrder="0"   
                  CustomerID="ALFKI">  
           <CompanyName>Alfreds Futterkiste</CompanyName>  
           <ContactName>Maria Anders</ContactName>  
        </Customer>  
    </diffgr:before>  
    <msdata:errors/>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 在中 **\<之前 >** 块中，没有 **\<顺序 >** 元素 (**diffgr: id ="顺序排列 1"**) 和一个 **\<客户 >** 元素 (**diffgr: id ="Customer1"**)。 这些元素表示数据库中的现有记录。 **\<DataInstance >** 元素不具有相应的记录 (具有相同 **diffgr: id**)。 这指示一个删除操作。  
  
#### <a name="to-test-the-diffgram"></a>测试 DiffGram  
  
1.  创建这些表中的**tempdb**数据库。  
  
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
  
2.  添加以下示例数据：  
  
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
  
3.  复制上面的 DiffGram，并将它粘贴到文本文件中。 在上一步所使用的文件夹中将该文件另存为 MyDiffGram.xml。  
  
4.  复制本主题上文所提供的 DiffGramSchema，并将其粘贴到文本文件中。 将该文件另存为 DiffGramSchema.xml。  
  
5.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行 DiffGram。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
## <a name="b-inserting-a-record-by-using-a-diffgram"></a>B. 使用 DiffGram 插入记录  
 在本示例中，DiffGram 在 Cust 表和 Ord 表中各插入一条记录。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"   
      sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
          xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
          xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
       <Customer diffgr:id="Customer1" msdata:rowOrder="0"    
                 diffgr:hasChanges="inserted" CustomerID="ALFKI">  
        <CompanyName>C3Company</CompanyName>  
        <ContactName>C3Contact</ContactName>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"  
               diffgr:hasChanges="inserted"   
               CustomerID="ALFKI" OrderID="1"/>  
      </Customer>  
    </DataInstance>  
  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 在这个 DiffGram **\<之前 >** 块未指定 （没有现有数据库标识的记录）。 有两个记录实例 (由标识 **\<客户>** 并 **\<顺序>** 中的元素 **\<DataInstance >** 块)，它将映射到 Cust 和 Ord 表，分别。 这两个元素指定**diffgr: haschanges**属性 (**hasChanges ="inserted"**)。 这指示一个插入操作。 在这个 DiffGram 中，如果您指定**hasChanges ="modified"**，则表示你想要修改不存在，这会导致错误的记录。  
  
#### <a name="to-test-the-diffgram"></a>测试 DiffGram  
  
1.  创建这些表中的**tempdb**数据库。  
  
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
  
2.  添加以下示例数据：  
  
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
  
3.  复制上面的 DiffGram，并将它粘贴到文本文件中。 在上一步所使用的文件夹中将该文件另存为 MyDiffGram.xml。  
  
4.  复制本主题上文所提供的 DiffGramSchema，并将其粘贴到文本文件中。 将该文件另存为 DiffGramSchema.xml。  
  
5.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行 DiffGram。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
## <a name="c-updating-an-existing-record-by-using-a-diffgram"></a>C. 使用 DiffGram 更新现有记录  
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
  
 **\<之前 >** 块包括 **\<客户 >** 元素 (**diffgr: id ="Customer1"**)。 **\<DataInstance >** 块包括相应 **\<客户 >** 元素具有相同 **id**。**\<客户 >** 中的元素 **\<NewDataSet >** 还指定了 **diffgr:haschanges="modified"**。 这表示更新操作，并且中的客户记录**Cust**相应地更新表。 请注意，如果**diffgr: haschanges**属性未指定，DiffGram 处理逻辑将忽略此元素，则不执行任何更新。  
  
#### <a name="to-test-the-diffgram"></a>测试 DiffGram  
  
1.  创建这些表中的**tempdb**数据库。  
  
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
  
2.  添加以下示例数据：  
  
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
  
3.  复制上面的 DiffGram，并将它粘贴到文本文件中。 在上一步所使用的文件夹中将该文件另存为 MyDiffGram.xml。  
  
4.  复制本主题上文所提供的 DiffGramSchema，并将其粘贴到文本文件中。 将该文件另存为 DiffGramSchema.xml。  
  
5.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行 DiffGram。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
## <a name="d-inserting-updating-and-deleting-records-by-using-a-diffgram"></a>D. 使用 DiffGram 插入、更新和删除记录  
 在本示例中，使用一个较为复杂的 DiffGram 执行插入、更新和删除操作。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                diffgr:hasChanges="modified"   
                CustomerID="ANATR">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Elizabeth Lincoln</ContactName>  
          <Order diffgr:id="Order2" msdata:rowOrder="1"   
               msdata:hiddenCustomerID="ANATR"   
               CustomerID="ANATR" OrderID="2"/>  
      </Customer>  
  
      <Customer diffgr:id="Customer3" msdata:rowOrder="2"   
                CustomerID="ANTON">  
         <CompanyName>Chop-suey Chinese</CompanyName>  
         <ContactName>Yang Wang</ContactName>  
         <Order diffgr:id="Order3" msdata:rowOrder="2"   
               msdata:hiddenCustomerID="ANTON"   
               CustomerID="ANTON" OrderID="3"/>  
      </Customer>  
      <Customer diffgr:id="Customer4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                CustomerID="AROUT">  
         <CompanyName>Around the Horn</CompanyName>  
         <ContactName>Thomas Hardy</ContactName>  
         <Order diffgr:id="Order4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                msdata:hiddenCustomerID="AROUT"   
               CustomerID="AROUT" OrderID="4"/>  
      </Customer>  
    </DataInstance>  
    <diffgr:before>  
      <Order diffgr:id="Order1" msdata:rowOrder="0"   
             msdata:hiddenCustomerID="ALFKI"   
             CustomerID="ALFKI" OrderID="1"/>  
      <Customer diffgr:id="Customer1" msdata:rowOrder="0"   
                CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                CustomerID="ANATR">  
        <CompanyName>Ana Trujillo Emparedados y helados</CompanyName>  
        <ContactName>Ana Trujillo</ContactName>  
      </Customer>  
    </diffgr:before>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 DiffGram 逻辑按如下方式处理此 DiffGram：  
  
-   根据 DiffGram 处理逻辑中的所有顶级元素 **\<之前 >** 阻止映射到相应的表，如映射架构中所述。  
  
-   **\<之前 >** 块都有 **\<顺序 >** 元素 (**dffgr:id ="顺序排列 1"**) 和一个 **\<客户>** 元素 (**diffgr: id ="Customer1"**) 它们没有中的没有相应元素 **\<DataInstance >** 块 （具有相同 ID)。 这指示一个删除操作，将从 Cust 表和 Ord 表中删除记录。  
  
-   **\<之前 >** 块都有 **\<客户 >** 元素 (**diffgr: id ="Customer2"**) 它们没有相应 **\<客户 >** 中的元素 **\<DataInstance >** 块 （具有相同 ID)。 中的元素 **\<DataInstance >** 块指定**diffgr: haschanges ="modified"**。 这是在其中针对客户 ANATR，CompanyName 和 ContactName 信息更新在使用中指定的值在 Cust 表中的更新操作 **\<DataInstance >** 块。  
  
-   **\<DataInstance >** 块都有 **\<客户 >** 元素 (**diffgr: id ="Customer3"**) 和一个 **\<顺序 >** 元素 (**diffgr: id ="Order3"**)。 两个元素都不指定**diffgr: haschanges**属性。 因此，DiffGram 处理逻辑将忽略这些元素。  
  
-   **\<DataInstance >** 块都有 **\<客户 >** 元素 (**diffgr: id ="Customer4"**) 和一个 **\<顺序 >** 元素 (**diffgr: id ="Order4"**) 为其没有中的相应元素\<之前 > 块。 中的这些元素 **\<DataInstance >** 块指定**diffgr: haschanges ="inserted"**。 因此，将在 Cust 表和 Ord 表中添加一条新记录。  
  
#### <a name="to-test-the-diffgram"></a>测试 DiffGram  
  
1.  创建以下表中的**tempdb**数据库。  
  
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
  
2.  添加以下示例数据：  
  
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
  
3.  复制上面的 DiffGram，并将它粘贴到文本文件中。 在上一步所使用的文件夹中将该文件另存为 MyDiffGram.xml。  
  
4.  复制本主题上文所提供的 DiffGramSchema，并将其粘贴到文本文件中。 将该文件另存为 DiffGramSchema.xml。  
  
5.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行 DiffGram。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
## <a name="e-applying-updates-by-using-a-diffgram-with-the-diffgrparentid-annotation"></a>E. 通过使用带有 diffgr:parentID 批注的 DiffGram 应用更新  
 此示例演示了如何**parentID** 中指定的批注 **\<之前 >** 中应用更新使用在 diffgram 的块。  
  
```  
<NewDataSet />  
<diffgr:before>  
   <Order diffgr:id="Order1" msdata:rowOrder="0" OrderID="2" />  
   <Order diffgr:id="Order3" msdata:rowOrder="2" OrderID="4" />  
  
   <OrderDetail diffgr:id="OrderDetail1"   
                diffgr:parentId="Order1"   
                msdata:rowOrder="0"   
                ProductID="13"   
                OrderID="2" />  
   <OrderDetail diffgr:id="OrderDetail3"   
                diffgr:parentId="Order3"  
                ProductID="77"  
                OrderID="4"/>  
</diffgr:before>  
</diffgr:diffgram>  
```  
  
 此 DiffGram 指定删除操作，因为只有 **\<之前 >** 块。 在 DiffGram 中， **parentID**批注用于指定订单和订单详细信息之间的父子关系。 当 SQLXML 删除记录时，它先从此关系标识的子表中删除记录，然后从相应的父表中删除记录。  
  
  
