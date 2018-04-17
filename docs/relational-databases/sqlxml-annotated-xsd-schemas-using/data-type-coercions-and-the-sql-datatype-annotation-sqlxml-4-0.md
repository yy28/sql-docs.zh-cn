---
title: '数据类型强制和 sql: datatype 批注 (SQLXML 4.0) |Microsoft 文档'
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- type attribute
- sql:datatype
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- xsd:type
- datatype annotation
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XSD schemas [SQLXML], mapping data types
ms.assetid: db192105-e8aa-4392-b812-9d727918c005
caps.latest.revision: 29
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8a2dc2c3d91eea67e9e08a87d5aa7735a1b45b1f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="data-type-coercions-and-the-sqldatatype-annotation-sqlxml-40"></a>数据类型强制和 sql:datatype 批注 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  在 XSD 架构中， **xsd:type**属性指定的元素或属性的 XSD 数据类型。 在 XSD 架构用于从数据库中提取数据时，指定的数据类型用于将数据格式化。  
  
 除了在架构中指定 XSD 类型，还可以指定 Microsoft[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用的数据类型**sql: datatype**批注。 **Xsd:type**和**sql: datatype**属性控制 XSD 数据类型之间的映射和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型。  
  
## <a name="xsdtype-attribute"></a>xsd:type 属性  
 你可以使用**xsd:type**特性来指定某个属性或元素映射到某一列的 XML 数据类型。 **Xsd:type**影响从服务器上以及执行 XPath 查询返回的文档。 针对包含的映射架构执行 XPath 查询时**xsd:type**，在处理查询时，XPath 使用指定的数据类型。 有关如何使用 XPath **xsd:type**，请参阅[将 XSD 数据类型映射 XPath 数据类型&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)。  
  
 在返回的文档中，所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型都转换为字符串表示形式。 某些数据类型需要其他转换。 下表列出了用于各种转换**xsd:type**值。  
  
|XSD 数据类型|SQL Server 转换|  
|-------------------|---------------------------|  
|Boolean|CONVERT(bit, COLUMN)|  
|日期|LEFT(CONVERT(nvarchar(4000), COLUMN, 126), 10)|  
|decimal|CONVERT(money, COLUMN)|  
|id/idref/idrefs|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|nmtoken/nmtokens|id-prefix + CONVERT(nvarchar(4000), COLUMN, 126)|  
|Time|SUBSTRING(CONVERT(nvarchar(4000), COLUMN, 126), 1+CHARINDEX(N'T', CONVERT(nvarchar(4000), COLUMN, 126)), 24)|  
|其他|无其他转换|  
  
> [!NOTE]  
>  返回的值的一些[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可能不是与使用指定的 XML 数据类型兼容**xsd:type**，因为此转换不可能 (例如，将"XYZ"转换为**十进制**数据类型) 或者是因为值超出了该数据类型的范围 (例如，-100000 转换为**UnsignedShort** XSD 类型)。 不兼容的类型转换可能导致无效的 XML 文档或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误。  
  
## <a name="mapping-from-sql-server-data-types-to-xsd-data-types"></a>从 SQL Server 数据类型映射到 XSD 数据类型  
 下表显示从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型到 XSD 数据类型的显式映射。 如果您知道 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 类型，此表将提供可以在 XSD 架构中指定的相应 XSD 类型。  
  
|SQL Server 数据类型|XSD 数据类型|  
|--------------------------|-------------------|  
|**bigint**|**长**|  
|**binary**|**base64Binary**|  
|**bit**|**boolean**|  
|**char**|**字符串**|  
|**datetime**|**dateTime**|  
|**decimal**|**decimal**|  
|**float**|**double**|  
|**image**|**base64Binary**|  
|**int**|**int**|  
|**money**|**decimal**|  
|**nchar**|**字符串**|  
|**ntext**|**字符串**|  
|**nvarchar**|**字符串**|  
|**numeric**|**decimal**|  
|**real**|**float**|  
|**smalldatetime**|**dateTime**|  
|**int**|**short**|  
|**smallmoney**|**decimal**|  
|**sql_variant**|**字符串**|  
|**sysname**|**字符串**|  
|**text**|**字符串**|  
|**timestamp**|**dateTime**|  
|**tinyint**|**unsignedByte**|  
|**varbinary**|**base64Binary**|  
|**varchar**|**字符串**|  
|**uniqueidentifier**|**字符串**|  
  
## <a name="sqldatatype-annotation"></a>sql:datatype 批注  
 **Sql: datatype**批注用于指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型; 此批注时，必须指定：  
  
-   要大容量加载到**dateTime** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]列从 XSD **dateTime**，**日期**，或**时间**类型。 在这种情况下，你必须确定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]列的数据类型使用**sql: datatype ="dateTime"**。 此规则也适用于 updategram。  
  
-   要插入的某个列的大容量加载[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **uniqueidentifier**类型和 XSD 值是一个 GUID，包括大括号 （{和}）。 当指定**sql: datatype ="uniqueidentifier"**，大括号会从值之前它将插入列中。 如果**sql: datatype**未指定，则使用大括号，并且插入或更新失败发送的值。  
  
-   XML 数据类型**base64Binary**映射到各种[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型 (**二进制**，**映像**，或**varbinary**)。 若要将 XML 数据类型映射**base64Binary**到特定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型，请使用**sql: datatype**批注。 此批注指定属性要映射到的列的显式 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型。 当正在数据库中存储数据时，这很有用。 通过指定**sql: datatype**批注，您可以标识显式[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型。  
  
 通常建议你指定**sql: datatype**架构中。  
  
## <a name="examples"></a>示例  
 若要创建使用以下示例的工作示例，必须满足某些要求。 有关详细信息，请参阅[要求运行 SQLXML 示例](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-xsdtype"></a>A. 指定 xsd:type  
 此示例演示如何 XSD**日期**通过使用指定的类型**xsd:type**架构中的属性影响生成的 XML 文档。 该架构提供 AdventureWorks 数据库中 Sales.SalesOrderHeader 表的 XML 视图。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader">  
     <xsd:complexType>  
       <xsd:attribute name="SalesOrderID" type="xsd:string" />   
       <xsd:attribute name="CustomerID"   type="xsd:string" />   
       <xsd:attribute name="OrderDate"    type="xsd:date" />   
       <xsd:attribute name="DueDate"  />   
       <xsd:attribute name="ShipDate"  type="xsd:time" />   
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 在该 XSD 架构中，有三个从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回日期值的属性。 当该架构：  
  
-   指定**xsd:type = 日期**上**OrderDate**属性，返回的值的日期部分[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为**OrderDate**显示属性。  
  
-   指定**xsd:type = 时间**上**ShipDate**特性，通过返回的值的时间部分[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为**ShipDate**显示属性。  
  
-   未指定**xsd:type**上**DueDate**属性，返回的相同值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]显示。  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>若要测试示例 XPath 查询根据架构  
  
1.  复制上面的架构代码，并将它粘贴到文本文件中。 将该文件另存为 xsdType.xml。  
  
2.  复制以下模板，并将它粘贴到文本文件中。 在保存 xsdType.xml 的相同目录中将文件另存为 xsdTypeT.xml。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="xsdType.xml">  
        /Order  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     为映射架构 (xsdType.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\xsdType.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[到执行 SQLXML 4.0 查询使用 ADO](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 下面是部分结果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="43659"   
         CustomerID="676"   
         OrderDate="2001-07-01"   
         DueDate="2001-07-13T00:00:00"   
         ShipDate="00:00:00" />   
  <Order SalesOrderID="43660"   
         CustomerID="117"   
         OrderDate="2001-07-01"   
         DueDate="2001-07-13T00:00:00"   
         ShipDate="00:00:00" />   
 ...  
</ROOT>  
```  
  
 这是等效的 XDR 架构：  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="Order" sql:relation="Sales.SalesOrderHeader">  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="CustomerID"  />  
    <AttributeType name="OrderDate" dt:type="date" />  
    <AttributeType name="DueDate" />  
    <AttributeType name="ShipDate" dt:type="time" />  
  
    <attribute type="SalesOrderID" sql:field="OrderID" />  
    <attribute type="CustomerID" sql:field="CustomerID" />  
    <attribute type="OrderDate" sql:field="OrderDate" />  
    <attribute type="DueDate" sql:field="DueDate" />  
    <attribute type="ShipDate" sql:field="ShipDate" />  
</ElementType>  
</Schema>  
```  
  
### <a name="b-specifying-sql-data-type-using-sqldatatype"></a>B. 使用 sql:datatype 指定 SQL 数据类型  
 有关工作示例，请参阅中的示例 G [XML 大容量加载示例&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)。 在此示例中，大容量加载包含“{”和“}”的 GUID 值。 在此示例中的架构指定**sql: datatype**来标识[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据类型作为**uniqueidentifier**。 此示例说明何时**sql: datatype**必须架构中指定。  
  
  
