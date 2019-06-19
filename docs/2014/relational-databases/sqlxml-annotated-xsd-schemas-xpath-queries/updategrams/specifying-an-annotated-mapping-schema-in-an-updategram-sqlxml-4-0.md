---
title: 在 Updategram (SQLXML 4.0) 中指定带批注的映射架构 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, updategrams
- data types [SQLXML], mapping schema in updategrams
- updategrams [SQLXML], annotated mapping schemas
- annotated XDR schemas, updategrams
- inverse attribute
- parent-child relationships [SQLXML]
- mapping-schema attribute
- mapping schema [SQLXML], updategrams
- sql:inverse
ms.assetid: 2e266ed9-4cfb-434a-af55-d0839f64bb9a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 627ab54ed35cbc0a43c5a0eac26a1397199edbd8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014665"
---
# <a name="specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-40"></a>在 updategram 中指定带批注的映射架构 (SQLXML 4.0)
  本主题说明如何使用在 updategram 中指定的映射架构（XSD 或 XDR）来处理更新。 在 updategram 中，您可以使用映射到表和列中的元素和属性在 updategram 中的带批注的映射架构的名称[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 在 updategram 中指定映射架构时，updategram 中指定的元素和属性名称必须映射为该映射架构的元素和属性。  
  
 若要指定映射架构，请使用`mapping-schema`的属性 **\<同步 >** 元素。 以下示例显示两个 updategram：其中一个使用简单映射架构，而另一个使用较复杂的架构。  
  
> [!NOTE]  
>  本文档假定您熟悉 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的模板和映射架构支持。 有关详细信息，请参阅[带批注的 XSD 架构简介&#40;SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md)。 有关使用 XDR 的旧版应用程序，请参阅[带批注的 XDR 架构&#40;在 SQLXML 4.0 中不推荐使用&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="dealing-with-data-types"></a>处理数据类型  
 如果架构指定了`image`， `binary`，或`varbinary`[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据类型 (通过使用`sql:datatype`)，且未指定 XML 数据类型，updategram 则假定 XML 数据类型是`binary base 64`。 如果数据类型为 `bin.base`，则必须显式指定类型（`dt:type=bin.base` 或 `type="xsd:hexBinary"`）。  
  
 如果架构指定了 `dateTime`、`date` 或 `time` XSD 数据类型，则还必须使用 `sql:datatype="dateTime"` 指定对应的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型。  
  
 处理的参数时[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]`money`类型，则必须显式指定`sql:datatype="money"`映射架构中的相应节点上。  
  
## <a name="examples"></a>示例  
 若要创建使用以下示例的工作示例，必须满足中指定的要求[运行 SQLXML 示例的要求](../../sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-creating-an-updategram-with-a-simple-mapping-schema"></a>A. 创建采用简单映射架构的 Updategram  
 以下 XSD 架构 (SampleSchema.xml) 是映射的映射架构 **\<客户 >** 到 Sales.Customer 表的元素：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
        <xsd:attribute name="CustID"    
                       sql:field="CustomerID"   
                       type="xsd:string" />  
        <xsd:attribute name="RegionID"    
                       sql:field="TerritoryID"    
                       type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 以下 updategram 在 Sales.Customer 表中插入一条记录，并使用前面的映射架构将此数据正确映射到表。 请注意，updategram 使用相同的元素名称， **\<客户 >** ，如在架构中定义。 这是强制性的，因为 updategram 会指定特定的架构。  
  
##### <a name="to-test-the-updategram"></a>测试 updategram  
  
1.  复制上面的架构代码，并将它粘贴到文本文件中。 将文件另存为 SampleUpdateSchema.xml。  
  
2.  复制下面的 updategram 模板，然后将其粘贴到文本文件中。 在您保存 SampleUpdateSchema.xml 的相同目录中将文件另存为 SampleUpdategram.xml。  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleUpdateSchema.xml">  
        <updg:before>  
          <Customer CustID="1" RegionID="1"  />  
        </updg:before>  
        <updg:after>  
          <Customer CustID="1" RegionID="2" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
     为映射架构 (SampleUpdateSchema.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下是等效的 XDR 架构：  
  
```  
<?xml version="1.0" ?>  
   <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
         xmlns:dt="urn:schemas-microsoft-com:datatypes"   
         xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
     <ElementType name="Customer" sql:relation="Sales.Customer" >  
       <AttributeType name="CustID" />  
       <AttributeType name="RegionID" />  
  
       <attribute type="CustID" sql:field="CustomerID" />  
       <attribute type="RegionID" sql:field="TerritoryID" />  
     </ElementType>  
   </Schema>   
```  
  
### <a name="b-inserting-a-record-by-using-the-parent-child-relationship-specified-in-the-mapping-schema"></a>B. 使用在映射架构中指定的父子关系插入记录  
 架构元素可以相互关联。 **\<Sql: relationship >** 元素指定架构元素之间的父-子关系。 此信息用于更新具有主键/外键关系的相应表。  
  
 以下映射架构 (SampleSchema.xml) 由两个元素组成 **\<顺序 >** 并 **\<OD >** :  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="OD"   
                     sql:relation="Sales.SalesOrderDetail"  
                     sql:relationship="OrderOD" >  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID"   type="xsd:integer" />  
              <xsd:attribute name="ProductID" type="xsd:integer" />  
             <xsd:attribute name="UnitPrice"  type="xsd:decimal" />  
             <xsd:attribute name="OrderQty"   type="xsd:integer" />  
             <xsd:attribute name="UnitPriceDiscount"   type="xsd:decimal" />  
  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
        <xsd:attribute name="SalesOrderID"  type="xsd:integer" />  
        <xsd:attribute name="OrderDate"  type="xsd:date" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 以下 updategram 使用此 XSD 架构添加新的订单详细记录 ( **\<OD >** 中的元素 **\<后 >** 块) 为订单 43860。 `mapping-schema` 属性用于指定 updategram 中的映射架构。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="SampleUpdateSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43860" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43860" >  
           <OD ProductID="753" UnitPrice="$10.00"  
               Quantity="5" Discount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>测试 updategram  
  
1.  复制上面的架构代码，并将它粘贴到文本文件中。 将文件另存为 SampleUpdateSchema.xml。  
  
2.  复制上面的 Updategram 模板，并将它粘贴到文本文件中。 在您保存 SampleUpdateSchema.xml 的相同目录中将文件另存为 SampleUpdategram.xml。  
  
     为映射架构 (SampleUpdateSchema.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 以下是等效的 XDR 架构：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="OD" sql:relation="Sales.SalesOrderDetail" >  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="ProductID" />  
    <AttributeType name="UnitPrice"  dt:type="fixed.14.4" />  
    <AttributeType name="OrderQty" />  
    <AttributeType name="UnitPriceDiscount" />  
  
    <attribute type="SalesOrderID" />  
    <attribute type="ProductID" />  
    <attribute type="UnitPrice" />  
    <attribute type="OrderQty" />  
    <attribute type="UnitPriceDiscount" />  
</ElementType>  
  
<ElementType name="Order" sql:relation="Sales.SalesOrderHeader" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="OrderDate" />  
  
    <attribute type="CustomerID" />  
    <attribute type="SalesOrderID" />  
    <attribute type="OrderDate" />  
    <element type="OD" >  
             <sql:relationship   
                   key-relation="Sales.SalesOrderHeader"  
                   key="SalesOrderID"  
                   foreign-key="SalesOrderID"  
                   foreign-relation="Sales.SalesOrderDetail" />  
    </element>  
</ElementType>  
</Schema>  
```  
  
### <a name="c-inserting-a-record-by-using-the-parent-child-relationship-and-inverse-annotation-specified-in-the-xsd-schema"></a>C. 使用在 XSD 架构中指定的父子关系和反转批注插入记录  
 此示例说明 updategram 逻辑如何使用在 XSD 中指定的父子关系来处理更新以及如何使用 `inverse` 批注。 有关详细信息`inverse`批注，请参阅[relationship 上指定 sql: inverse 属性&#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)。  
  
 下表是在此示例假定**tempdb**数据库：  
  
-   `Cust (CustomerID, CompanyName)`，其中 `CustomerID` 为主键。  
  
-   `Ord (OrderID, CustomerID)`，其中 `CustomerID` 是引用 `CustomerID` 表中的 `Cust` 主键的外键。  
  
 updategram 使用以下 XSD 架构将记录插入到 Cust 和 Ord 表中：  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
       <sql:relationship name="OrdCust" inverse="true"  
                  parent="Ord"  
                  parent-key="CustomerID"  
                  child-key="CustomerID"  
                  child="Cust"/>  
  </xsd:appinfo>  
</xsd:annotation>  
  
<xsd:element name="Order" sql:relation="Ord">  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element ref="Customer" sql:relationship="OrdCust"/>  
    </xsd:sequence>  
    <xsd:attribute name="OrderID"   type="xsd:int"/>  
    <xsd:attribute name="CustomerID" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:element>  
  
<xsd:element name="Customer" sql:relation="Cust">  
  <xsd:complexType>  
     <xsd:attribute name="CustomerID"  type="xsd:string"/>  
    <xsd:attribute name="CompanyName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:element>  
  
</xsd:schema>  
```  
  
 在此示例中，XSD 架构包含 **\<客户 >** 并 **\<顺序 >** 元素，并指定两个元素之间的父-子关系。 它标识 **\<顺序 >** 与父元素和 **\<客户 >** 作为子元素。  
  
 updategram 处理逻辑使用父子关系相关信息来确定将记录插入到表中的顺序。 在此示例中，updategram 逻辑首先尝试向 Ord 表插入记录 (因为 **\<顺序 >** 父级)，然后尝试向 Cust 表插入记录 (因为 **\<客户 >** 的子级)。 但是，鉴于数据库表架构中包含的主键/外键信息，此插入操作将导致在数据库中的外键冲突，继而导致插入失败。  
  
 若要指示 updategram 逻辑在更新操作期间反转父子关系`inverse`指定批注 **\<关系 >** 元素。 这会导致首先向 Cust 表添加记录，然后再向 Ord 表添加记录，并且该操作将成功。  
  
 以下 updategram 使用指定的 XSD 架构向 Ord 表插入订单 (OrderID=2)，并向 Cust 表插入客户 (CustomerID='AAAAA')：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="SampleUpdateSchema.xml" >  
    <updg:before/>  
    <updg:after>  
      <Order OrderID="2" CustomerID="AAAAA" >  
        <Customer CustomerID="AAAAA" CompanyName="AAAAA Company" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>测试 updategram  
  
1.  创建这些表中的**tempdb**数据库：  
  
    ```  
    USE tempdb  
    CREATE TABLE Cust(CustomerID varchar(5) primary key,   
                      CompanyName varchar(20))  
    GO  
    CREATE TABLE Ord (OrderID int primary key,   
                      CustomerID varchar(5) references Cust(CustomerID))  
    GO  
    ```  
  
2.  复制上面的架构代码，并将它粘贴到文本文件中。 将文件另存为 SampleUpdateSchema.xml。  
  
3.  复制上面的 Updategram 模板，并将它粘贴到文本文件中。 在您保存 SampleUpdateSchema.xml 的相同目录中将文件另存为 SampleUpdategram.xml。  
  
     为映射架构 (SampleUpdateSchema.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
4.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
## <a name="see-also"></a>请参阅  
 [Updategram 安全注意事项&#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
