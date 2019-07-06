---
title: 更新数据使用 XML Updategram (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREF type attribute [SQLXML]
- before attribute
- <sync> block
- <after> block
- id attribute
- <before> block
- updg:after attribute
- mapping-schema attribute
- IDREFS type attribute [SQLXML]
- updg:id attribute
- multiple record updates
- after attribute
- updategrams [SQLXML], updating data
- updg:before attribute
- record updates [SQLXML]
ms.assetid: 90ef8a33-5ae3-4984-8259-608d2f1d727f
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4b9dada396889ebad2342e8bcb6e46f60663079d
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2019
ms.locfileid: "67585904"
---
# <a name="updating-data-using-xml-updategrams-sqlxml-40"></a>使用 XML Updategram 更新数据 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  更新现有数据时，必须指定 **\<之前 >** 并 **\<后 >** 块。 中指定的元素 **\<之前 >** 并 **\<后 >** 块描述所需的更改。 Updategram 使用在中指定的元素 **\<之前 >** 块来标识数据库中的现有记录。 中的相应元素 **\<后 >** 块指示执行更新操作后应如何查找记录的。 中的信息，updategram 创建与匹配的 SQL 语句 **\<后 >** 块。 然后，Updategram 使用该语句更新数据库。  
  
 以下是 Updategram 的更新操作格式：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
      <ElementName [updg:id="value"] .../>  
      [<ElementName [updg:id="value"] .../> ... ]  
   </updg:before>  
   <updg:after>  
      <ElementName [updg:id="value"] ... />  
      [<ElementName [updg:id="value"] .../> ...]  
   </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 **\<updg:before>**  
 中的元素 **\<之前 >** 块标识数据库表中的现有记录。  
  
 **\<updg:after>**  
 中的元素 **\<后 >** 块描述中指定的记录如何 **\<之前 >** 块应查找后进行更新。  
  
 **映射架构**属性标识要由 updategram 的映射架构。 如果 updategram 指定映射架构，元素和属性名称中指定 **\<之前 >** 并 **\<后 >** 块必须与架构中的名称匹配。 该映射架构将这些元素或属性名称映射到数据库表和列名称。  
  
 如果 Updategram 不指定架构，则 Updategam 将使用默认映射。 在默认映射，  **\<ElementName >** updategram 映射到数据库表和子元素或属性映射到数据库列中指定。  
  
 中的元素 **\<之前 >** 块必须与数据库中只有一个表行匹配。 如果该元素与多个表行匹配，或与任何表行不匹配，则 updategram 返回错误，并取消整个 **\<同步 >** 块。  
  
 Updategram 可以包括多个 **\<同步 >** 块。 每个 **\<同步 >** 块均被视为一个事务。 每个 **\<同步 >** 块可以有多个 **\<之前 >** 并 **\<后 >** 块。 例如，如果要更新两个现有记录，则可以指定两个 **\<之前 >** 并 **\<后 >** 对，一个用于每个要更新的记录。  
  
## <a name="using-the-updgid-attribute"></a>使用 updg:id 属性  
 如果在中指定多个元素 **\<之前 >** 并 **\<后 >** 块，使用**updg: id**特性标记中的行 **\<之前 >** 并 **\<后 >** 块。 处理逻辑使用此信息来确定中的什么记录 **\<之前 >** 块中的什么记录对 **\<后 >** 块。  
  
 **Updg: id**属性不需要 （尽管建议这样做），如果存在以下任一：  
  
-   指定的映射架构中的元素具有**sql:key-字段**在其上定义特性。  
  
-   为 Updategram 中的键字段提供了一个或多个特定值。  
  
 如果是这种情况，则 updategram 将使用中指定的键列**sql:key-字段**中的元素进行配对 **\<之前 >** 并 **\<后 >** 块。  
  
 如果映射架构未标识键列 (通过使用**sql:key-字段**) 或者 updategram 要更新键列值，您必须指定**updg: id**。  
  
 中标识的记录 **\<之前 >** 并 **\<后 >** 块没有处于相同的顺序。 **Updg: id**属性强制中指定的元素之间的关联 **\<之前 >** 并 **\<后 >** 块。  
  
 如果指定中的有一个元素 **\<之前 >** 块和中的只能有一个相应元素 **\<后 >** 阻止，请使用**updg: id**不是必需的。 但是，建议您指定**updg: id**仍以避免多义性。  
  
## <a name="examples"></a>示例  
 在使用 Updategram 示例之前，请注意以下事项：  
  
-   大多数示例使用默认映射（即，未在 updategram 中指定任何映射架构）。 有关使用映射架构的 updategram 的更多示例，请参阅[在 Updategram 中指定带批注的映射架构&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
-   大多数示例使用 AdventureWorks 示例数据库。 已对该数据库中的表应用所有更新。 您可以还原 AdventureWorks 数据库。  
  
### <a name="a-updating-a-record"></a>A. 更新记录  
 以下 Updategram 将 AdventureWorks 数据库的 Person.Contact 表中的雇员姓氏更新为 Fuller。 Updategram 不指定任何映射架构，因此，Updategram 使用默认映射。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
<updg:before>  
   <Person.Contact ContactID="1" />  
</updg:before>  
<updg:after>  
   <Person.Contact LastName="Abel-Achong" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 该记录中所述 **\<之前 >** 块表示数据库中的当前记录。 Updategram 使用的列的值中指定的所有 **\<之前 >** 块来搜索记录。 在该 updategram **\<之前 >** 块仅提供 ContactID 列; 因此，updategram 仅使用值以搜索记录。 如果要将 LastName 值添加到该块，则 Updategram 会同时使用 ContactID 和 LastName 值执行搜索。  
  
 在该 updategram **\<后 >** 块提供的 LastName 列值，因为这是正在更改的唯一值。  
  
##### <a name="to-test-the-updategram"></a>测试 updategram  
  
1.  复制上面的 Updategram 模板，并将它粘贴到文本文件中。 将该文件另存为 UpdateLastName.xml。  
  
2.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 以执行 updategram。  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

     For more information, see [Using ADO to Execute SQLXML 4.0 Queries](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="b-updating-multiple-records-by-using-the-updgid-attribute"></a>B. 使用 updg:id 属性更新多个记录  
 在该示例中，Updategram 对 AdventureWorks 数据库中的 HumanResources.Shift 表执行两次更新：  
  
-   它将 7:00AM 开始的原始白班的名称从“Day”更改为“Early Morning”。  
  
-   它插入名为“Late Morning”的从 10:00AM 开始的新班。  
  
 在 updategram 中， **updg: id**属性将创建中的元素之间的关联 **\<之前 >** 并 **\<后 >** 块。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift updg:id="x" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift updg:id="y" Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
      <HumanResources.Shift updg:id="x" Name="Early Morning" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 请注意如何**updg: id**特性对的第一个实例\<HumanResources.Shift > 元素中的 **\<之前 >** 块第二个实例\<HumanResources.Shift > 中的元素 **\<后 >** 块。  
  
##### <a name="to-test-the-updategram"></a>测试 updategram  
  
1.  复制上面的 Updategram 模板，并将它粘贴到文本文件中。 将该文件另存为 UpdateMultipleRecords.xml。  
  
2.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 以执行 updategram。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="c-specifying-multiple-before-and-after-blocks"></a>C. 指定多个\<之前 > 和\<后 > 块  
 若要避免混淆，您可以编写 updategram 示例 B 中使用多个 **\<之前 >** 并 **\<后 >** 块对。 指定 **\<之前 >** 并 **\<后 >** 对是指定具有最不易混淆的多个更新的一种方法。 此外，如果每个的 **\<之前 >** 并 **\<后 >** 块指定最多一个元素，无需使用**updg: id**属性.  
  
> [!NOTE]  
>  若要形成配对， **\<后 >** 标记必须紧跟在其对应 **\<之前 >** 标记。  
  
 在以下 updategram 中，第一个 **\<之前 >** 并 **\<后 >** 对将更新白班白班的名称。 第二对将插入新的轮班记录。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
       <HumanResources.Shift ShiftID="1" Name="Day" />  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Early Morning" />  
    </updg:after>  
    <updg:before>  
    </updg:before>  
    <updg:after>  
      <HumanResources.Shift Name="Late Morning"   
                            StartTime="1900-01-01 10:00:00.000"  
                            EndTime="1900-01-01 18:00:00.000"  
                            ModifiedDate="2004-06-01 00:00:00.000"/>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>测试 updategram  
  
1.  复制上面的 Updategram 模板，并将它粘贴到文本文件中。 将该文件另存为 UpdateMultipleBeforeAfter.xml。  
  
2.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 以执行 updategram。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="d-specifying-multiple-sync-blocks"></a>D. 指定多个\<同步 > 块  
 可以指定多个 **\<同步 >** updategram 中的块。 每个 **\<同步 >** 指定的块是独立的事务。  
  
 在以下 updategram 中，第一个 **\<同步 >** 块更新 Sales.Customer 表中的记录。 出于简化原因，Updategram 仅指定必需的列值：标识值 (CustomerID) 和要更新的值 (SalesPersonID)。  
  
 第二个 **\<同步 >** 块将两条记录添加到 Sales.SalesOrderHeader 表。 对于该表，SalesOrderID 是 IDENTITY 类型的列。 因此，updategram 不指定 SalesOrderID 的值中的每个\<Sales.SalesOrderHeader > 元素。  
  
 指定多个 **\<同步 >** 块是很有用因为如果第二个 **\<同步 >** 块 （事务） 未能将记录添加到 Sales.SalesOrderHeader 表第一个 **\<同步 >** 块仍然可以更新 Sales.Customer 表中的客户记录。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
      <Sales.Customer CustomerID="1" SalesPersonID="280" />  
    </updg:before>  
    <updg:after>  
      <Sales.Customer CustomerID="1" SalesPersonID="283" />  
    </updg:after>  
  </updg:sync>  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
   <Sales.SalesOrderHeader   
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="01010101-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-08 00:00:00.000" />  
   <Sales.SalesOrderHeader  
             CustomerID="1"  
             RevisionNumber="1"  
             OrderDate="2004-07-01 00:00:00.000"  
             DueDate="2004-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="1000.0000"  
             TaxAmt="0.0000"  
             Freight="0.0000"  
             rowguid="10101010-2222-3333-4444-556677889900"  
             ModifiedDate="2004-07-09 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>测试 updategram  
  
1.  复制上面的 Updategram 模板，并将它粘贴到文本文件中。 将文件另存为 UpdateMultipleSyncs.xml。  
  
2.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 以执行 updategram。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
### <a name="e-using-a-mapping-schema"></a>E. 使用映射架构  
 在此示例中，updategram 指定映射架构通过使用**映射架构**属性。 （没有默认映射；就是说，由映射架构提供所需的映射，将 Updategram 中的元素和属性映射到数据库表和列。）  
  
 在 Updategram 中指定的元素和属性将引用映射架构中的元素和属性。  
  
 以下 XSD 映射架构有 **\<客户 >** ， **\<顺序 >** ，以及 **\<OD >** 将映射到元素数据库中的 Sales.Customer、 Sales.SalesOrderHeader 和 Sales.SalesOrderDetail 表。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustomerOrder"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustomerOrder" >  
           <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OD"   
                             sql:relation="Sales.SalesOrderDetail"  
                             sql:relationship="OrderOD" >  
                 <xsd:complexType>  
                  <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                  <xsd:attribute name="ProductID" type="xsd:integer" />  
                  <xsd:attribute name="UnitPrice" type="xsd:decimal" />  
                  <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  <xsd:attribute name="UnitPriceDiscount" type="xsd:decimal" />   
                 </xsd:complexType>  
                </xsd:element>  
              </xsd:sequence>  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="OrderDate" type="xsd:date" />  
           </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 以下 Updategram 指定该映射架构 (UpdategramMappingSchema.xml)。 该 Updategram 在 Sales.SalesOrderDetail 表中为特定顺序添加顺序细节项。 该 updategram 包括嵌套的元素：  **\<OD >** 元素嵌套在 **\<顺序 >** 元素。 在映射架构中指定了这两个元素之间的主键/外键关系。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="UpdategramMappingSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43659" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43659" >  
          <OD ProductID="776" UnitPrice="2329.0000"  
              OrderQty="2" UnitPriceDiscount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>测试 updategram  
  
1.  复制上面的映射架构，并将它粘贴到文本文件中。 将该文件另存为 UpdategramMappingSchema.xml。  
  
2.  复制上面的 Updategram 模板，并将它粘贴到文本文件中。 在用于保存映射架构 (UpdategramMappingSchema.xml) 的相同文件夹中将该文件另存为 UpdateWithMappingSchema.xml。  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 以执行 updategram。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 有关使用映射架构的 updategram 的更多示例，请参阅[在 Updategram 中指定带批注的映射架构&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
### <a name="f-using-a-mapping-schema-with-idrefs-attributes"></a>F. 将 IDREFS 属性与映射架构一起使用  
 该示例说明 Updategram 如何在映射架构中使用 IDREFS 属性以更新多个表中的记录。 对于该示例，假定数据库由以下表组成：  
  
-   Student(StudentID, LastName)  
  
-   Course(CourseID, CourseName)  
  
-   Enrollment(StudentID, CourseID)  
  
 由于学生可以注册参加很多课程，而且一种课程可以有很多学生，因此需要用第三个表 Enrollment 表以表示该 M:N 关系。  
  
 以下 XSD 映射架构通过使用提供的表的 XML 视图 **\<学生 >** ， **\<课程 >** ，以及 **\<注册>** 元素。 **IDREFS**属性映射架构中的指定这些元素之间的关系。 **StudentIDList**特性，可以在 **\<课程 >** 元素是**IDREFS**类型属性，它引用 Enrollment 表中的 StudentID 列。 同样， **enrolledin 属性**特性，可以在 **\<学生 >** 元素是**IDREFS**类型属性，它是指在注册中的 CourseID 列表。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="StudentEnrollment"  
          parent="Student"  
          parent-key="StudentID"  
          child="Enrollment"  
          child-key="StudentID" />  
  
    <sql:relationship name="CourseEnrollment"  
          parent="Course"  
          parent-key="CourseID"  
          child="Enrollment"  
          child-key="CourseID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Course" sql:relation="Course"   
                             sql:key-fields="CourseID" >  
    <xsd:complexType>  
    <xsd:attribute name="CourseID"  type="xsd:string" />   
    <xsd:attribute name="CourseName"   type="xsd:string" />   
    <xsd:attribute name="StudentIDList" sql:relation="Enrollment"  
                 sql:field="StudentID"  
                 sql:relationship="CourseEnrollment"   
                                     type="xsd:IDREFS" />  
  
    </xsd:complexType>  
  </xsd:element>  
  <xsd:element name="Student" sql:relation="Student" >  
    <xsd:complexType>  
    <xsd:attribute name="StudentID"  type="xsd:string" />   
    <xsd:attribute name="LastName"   type="xsd:string" />   
    <xsd:attribute name="EnrolledIn" sql:relation="Enrollment"  
                 sql:field="CourseID"  
                 sql:relationship="StudentEnrollment"   
                                     type="xsd:IDREFS" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 一旦在 Updategram 中指定该架构，并在 Course 表中插入记录，则 Updategram 将在 Course 表中插入新的课程记录。 如果为 StudentIDList 属性指定一个或多个新学生 ID，则 Updategram 还将在 Enrollment 表中为每个新学生插入记录。 该 Updategram 将确保不向 Enrollment 表添加重复项。  
  
##### <a name="to-test-the-updategram"></a>测试 updategram  
  
1.  在虚拟根目录中所指定的数据库内创建这些表：  
  
    ```  
    CREATE TABLE Student(StudentID varchar(10) primary key,   
                         LastName varchar(25))  
    CREATE TABLE Course(CourseID varchar(10) primary key,   
                        CourseName varchar(25))  
    CREATE TABLE Enrollment(StudentID varchar(10)   
                                      references Student(StudentID),  
                           CourseID varchar(10)   
                                      references Course(CourseID))  
    ```  
  
2.  添加以下示例数据：  
  
    ```  
    INSERT INTO Student VALUES ('S1','Davoli')  
    INSERT INTO Student VALUES ('S2','Fuller')  
  
    INSERT INTO Course VALUES  ('CS101', 'C Programming')  
    INSERT INTO Course VALUES  ('CS102', 'Understanding XML')  
  
    INSERT INTO Enrollment VALUES ('S1', 'CS101')  
    INSERT INTO Enrollment VALUES ('S1', 'CS102')  
    ```  
  
3.  复制上面的映射架构，并将它粘贴到文本文件中。 将该文件另存为 SampleSchema.xml。  
  
4.  将 Updategram (SampleUpdategram) 保存到上一步中用于保存映射架构的相同文件夹中。 （该 Updategram 从 CS102 课程中删除 StudentID="1" 的学生。）  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
5.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 以执行 updategram。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
6.  按照前面描述的步骤，保存并执行以下 Updategram。 该 Updategram 在 Enrollment 表中添加记录，从而将 StudentID="1" 的学生重新添加到 CS102 课程中。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101" />  
        </updg:before>  
        <updg:after >  
            <Student updg:id="x" StudentID="S1" LastName="Davolio"  
                                 EnrolledIn="CS101 CS102" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
7.  按照前面描述的步骤，保存并执行下一个 Updategram。 该 Updategram 插入三个新学生，并将他们注册到 CS101 课程。 同样，IDREFS 关系将在 Enrollment 表中插入记录。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleSchema.xml" >  
        <updg:before>  
           <Course updg:id="y" CourseID="CS101"   
                               CourseName="C Programming" />  
        </updg:before>  
        <updg:after >  
           <Student updg:id="x1" StudentID="S3" LastName="Leverling" />  
           <Student updg:id="x2" StudentID="S4" LastName="Pecock" />  
           <Student updg:id="x3" StudentID="S5" LastName="Buchanan" />  
           <Course updg:id="y" CourseID="CS101"  
                               CourseName="C Programming"  
                               StudentIDList="S3 S4 S5" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
 以下是等效的 XDR 架构：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ElementType name="Enrollment" sql:relation="Enrollment" sql:key-fields="StudentID CourseID">  
    <AttributeType name="StudentID" dt:type="id" />  
    <AttributeType name="CourseID" dt:type="id" />  
  
    <attribute type="StudentID" />  
    <attribute type="CourseID" />  
  </ElementType>  
  <ElementType name="Course" sql:relation="Course" sql:key-fields="CourseID">  
    <AttributeType name="CourseID" dt:type="id" />  
    <AttributeType name="CourseName" />  
  
    <attribute type="CourseID" />  
    <attribute type="CourseName" />  
  
    <AttributeType name="StudentIDList" dt:type="idrefs" />  
    <attribute type="StudentIDList" sql:relation="Enrollment" sql:field="StudentID" >  
        <sql:relationship  
                key-relation="Course"  
                key="CourseID"  
                foreign-relation="Enrollment"  
                foreign-key="CourseID" />  
    </attribute>  
  
  </ElementType>  
  <ElementType name="Student" sql:relation="Student">  
    <AttributeType name="StudentID" dt:type="id" />  
     <AttributeType name="LastName" />  
  
    <attribute type="StudentID" />  
    <attribute type="LastName" />  
  
    <AttributeType name="EnrolledIn" dt:type="idrefs" />  
    <attribute type="EnrolledIn" sql:relation="Enrollment" sql:field="CourseID" >  
        <sql:relationship  
                key-relation="Student"  
                key="StudentID"  
                foreign-relation="Enrollment"  
                foreign-key="StudentID" />  
    </attribute>  
  
    <element type="Enrollment" sql:relation="Enrollment" >  
        <sql:relationship key-relation="Student"  
                          key="StudentID"  
                          foreign-relation="Enrollment"  
                          foreign-key="StudentID" />  
    </element>  
  </ElementType>  
  
</Schema>  
```  
  
 有关使用映射架构的 updategram 的更多示例，请参阅[在 Updategram 中指定带批注的映射架构&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
## <a name="see-also"></a>请参阅  
 [Updategram 安全注意事项&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
