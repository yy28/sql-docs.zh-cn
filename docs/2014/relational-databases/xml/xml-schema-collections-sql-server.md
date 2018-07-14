---
title: XML 架构集合 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- XSD schemas [SQL Server]
- xml_schema_namespace function
- XML schema collections [SQL Server], about XML schema collections
- metadata [SQL Server], XML schema collections
- queries [XML in SQL Server], XML schema collections
- schema collections [SQL Server]
- schemas [SQL Server], XML
- XML [SQL Server], schema collections
- XML schema collections [SQL Server]
- schema collections [SQL Server], about XML schema collections
ms.assetid: 659d41aa-ccec-4554-804a-722a96ef25c2
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 05b266a67aaff2a381e181ca85290c45af177225
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37221087"
---
# <a name="xml-schema-collections-sql-server"></a>XML 架构集合 (SQL Server)
  主题中所述[xml &#40;TRANSACT-SQL&#41;](/sql/t-sql/xml/xml-transact-sql)，SQL Server 提供的 XML 数据进行本机存储`xml`数据类型。 您可以选择将与变量或列的关联的 XSD 架构`xml`通过 XML 架构集合的类型。 XML 架构集合存储导入的 XML 架构，然后用于执行以下操作：  
  
-   验证 XML 实例  
  
-   类型化在数据库中存储的 XML 数据  
  
 请注意，XML 架构集合是一个类似于数据库表的元数据实体。 您可以创建、修改和删除它们。 [CREATE XML SCHEMA COLLECTION (Transact-SQL)](/sql/t-sql/statements/create-xml-schema-collection-transact-sql) 语句中指定的架构将自动导入到新建的 XML 架构集合对象中。 通过使用 [ALTER XML SCHEMA COLLECTION (Transact-SQL)](/sql/t-sql/statements/alter-xml-schema-collection-transact-sql) 语句，可以将其他架构或架构组件导入到数据库中的现有集合对象。  
  
 如主题[类型化与非类型化的 XML](../xml/compare-typed-xml-to-untyped-xml.md) 中所述，存储在与架构关联的列或变量中的 XML 称为**类型化的** XML，因为该架构为实例数据提供了必要的数据类型信息。 SQL Server 使用此类型信息优化数据存储。  
  
 查询处理引擎也使用该架构进行类型检查并优化查询和数据修改。  
  
 此外，SQL Server 使用相关联的 XML 架构集合的情况下键入`xml`，来验证 XML 实例。 如果 XML 实例符合架构，则数据库允许该实例存储在包含其类型信息的系统中。 否则，它将拒绝该实例。  
  
 可以使用内部函数 XML_SCHEMA_NAMESPACE 检索数据库中存储的架构集合。 有关详细信息，请参阅 [查看存储 XML 架构集合](../xml/view-a-stored-xml-schema-collection.md)。  
  
 还可以使用 XML 架构集合类型化 XML 变量、参数和列。  
  
##  <a name="ddl"></a> 用于管理架构集合的 DDL  
 可以在数据库中创建 XML 架构集合并将其关联的变量和列与`xml`类型。 为了管理数据库中的架构集合， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了下列 DDL 语句：  
  
-   [CREATE XML SCHEMA COLLECTION (Transact-SQL)](/sql/t-sql/statements/create-xml-schema-collection-transact-sql) 可将架构组件导入到数据库。  
  
-   [ALTER XML SCHEMA COLLECTION (Transact-SQL)](/sql/t-sql/statements/alter-xml-schema-collection-transact-sql) 修改现有 XML 架构集合中的架构组件。  
  
-   [DROP XML SCHEMA COLLECTION (Transact-SQL)](/sql/t-sql/statements/drop-xml-schema-collection-transact-sql) 删除整个 XML 架构集合及其所有组件。  
  
 若要使用 XML 架构集合及其包含的架构，必须首先使用 CREATE XML SCHEMA COLLECTION 语句创建架构集合及其包含的架构。 创建架构集合后，您可以创建的变量和列`xml`键入并将其与关联的架构集合。 注意，创建架构集合之后，各种架构组件存储在元数据中。 还可以使用 ALTER XML SCHEMA COLLECTION 向现有架构添加更多组件或向现有集合添加新架构。  
  
 若要删除架构集合，请使用 DROP XML SCHEMA COLLECTION 语句。 它将删除包含在集合中的所有架构并删除集合对象。 请注意，只有在满足 [DROP XML SCHEMA COLLECTION (Transact-SQL)](/sql/t-sql/statements/drop-xml-schema-collection-transact-sql) 中所述的条件时，才能删除架构集合。  
  
##  <a name="components"></a> 了解架构组件  
 使用 CREATE XML SCHEMA COLLECTION 语句时，将把各种架构组件导入数据库中。 架构组件包括架构元素、属性和类型定义。 使用 DROP XML SCHEMA COLLECTION 语句时，将删除整个集合。  
  
 CREATE XML SCHEMA COLLECTION 将把架构组件保存到各种系统表中。  
  
 例如，请看下面的架构：  
  
```  
<?xml version="1.0"?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            targetNamespace="uri:Cust_Orders2"  
            xmlns="uri:Cust_Orders2" >  
  <xsd:attribute name="SomeAttribute" type="xsd:int" />  
  <xsd:complexType name="SomeType" />  
  <xsd:complexType name="OrderType" >  
    <xsd:sequence>  
      <xsd:element name="OrderDate" type="xsd:date" />  
      <xsd:element name="RequiredDate" type="xsd:date" />  
      <xsd:element name="ShippedDate" type="xsd:date" />  
    </xsd:sequence>  
    <xsd:attribute name="OrderID" type="xsd:ID" />  
    <xsd:attribute name="CustomerID"  />  
    <xsd:attribute name="EmployeeID"  />  
  </xsd:complexType>  
  <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order" type="OrderType"  
                     maxOccurs="unbounded" />  
       </xsd:sequence>  
      <xsd:attribute name="CustomerID" type="xsd:string" />  
      <xsd:attribute name="OrderIDList" type="xsd:IDREFS" />  
  </xsd:complexType>  
  <xsd:element name="Customer" type="CustomerType" />  
</xsd:schema>  
```  
  
 以上架构显示了可以存储在数据库中的不同类型的组件。 其中包括 `SomeAttribute`、 `SomeType`、 `OrderType`、 `CustomerType`、 `Customer`、 `Order`、 `CustomerID`、 `OrderID`、 `OrderDate`、 `RequiredDate`以及 `ShippedDate`。  
  
### <a name="component-categories"></a>组件类别  
 数据库中存储的架构组件分为下列类别：  
  
-   ELEMENT  
  
-   ATTRIBUTE  
  
-   TYPE（用于简单或复杂类型）  
  
-   ATTRIBUTEGROUP  
  
-   MODELGROUP  
  
 例如：  
  
-   **SomeAttribute** 是 ATTRIBUTE 组件。  
  
-   **SomeType**、 **OrderType**和 **CustomerType** 是 TYPE 组件。  
  
-   **Customer** 是 ELEMENT 组件。  
  
 将架构导入数据库时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会存储架构本身。 相反， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会存储各种不同的组件。 也就是说，不存储 \<Schema> 标记，仅保存在其中定义的组件。 不存储所有的架构元素。 如果 \<Schema> 标记包含指定其组件默认行为的属性，则在导入过程中，将把这些属性移动到其中的架构组件，如下表所示。  
  
|属性名称|行为|  
|--------------------|--------------|  
|**attributeFormDefault**|应用于架构中所有属性声明的 **form** 属性，此架构中不存在此属性并且将值设置为 **attributeFormDefault** 属性的值。|  
|**elementFormDefault**|应用于架构中所有元素声明的 **form** 属性，此架构中不存在此属性并且将值设置为 **elementFormDefault** 属性的值。|  
|**blockDefault**|应用于所有元素声明和类型定义的 **block** 属性，这些声明和定义中不存在此属性并且将值设置为 **blockDefault** 属性的值。|  
|**finalDefault**|应用于所有元素声明和类型定义的 **final** 属性，这些声明和定义中不存在此属性并且将值设置为 **finalDefault** 属性的值。|  
|**targetNamespace**|有关属于目标命名空间的组件的信息存储在元数据中。|  
  
##  <a name="perms"></a> XML 架构集合的权限  
 您必须具有必要的权限才能执行下列操作：  
  
-   创建/加载 XML 架构集合  
  
-   修改 XML 架构集合  
  
-   删除 XML 架构集合  
  
-   使用 XML 架构集合来键入`xml`类型列、 变量和参数，或在表或列约束中使用它  
  
 SQL Server 安全模式允许对每个对象使用 CONTROL 权限。 此权限的被授权者将获得对象的其他所有权限。 对象的所有者也拥有对象的所有权限。  
  
 对象上的 CONTROL 权限的所有者和被授权者可以授予对象的任何权限。 指定 WITH GRANT OPTION 后，不是所有者并且没有 CONTROL 权限的用户也可以授予对象的权限。 例如，假定用户 A 通过 WITH GRANT OPTION 对 XML 架构集合 S 具有 REFERENCES 权限，但对 S 没有其他任何权限。用户 A 可以授予用户 B 架构集合 S 的 REFERENCES 权限。  
  
 安全模式也允许使用这些权限来创建和使用 XML 架构集合或将所有权从一个用户传递到另一个用户。 下列主题说明了 XML 架构集合权限。  
  
-   [授予对 XML 架构集合的权限](../xml/grant-permissions-on-an-xml-schema-collection.md)  
  
     本主题讨论了如何授予创建 XML 架构集合的权限和如何授予 XML 架构集合对象的权限。  
  
-   [撤消对 XML 架构集合的权限](../xml/revoke-permissions-on-an-xml-schema-collection.md)  
  
     本主题讨论了如何使用撤消权限来防止创建 XML 架构集合和如何撤消 XML 架构集合对象的权限。  
  
-   [拒绝对 XML 架构集合的权限](../xml/deny-permissions-on-an-xml-schema-collection.md)  
  
     本主题讨论了如何拒绝创建 XML 架构集合的权限和如何拒绝 XML 架构集合对象的权限。  
  
##  <a name="info"></a> 获取有关 XML 架构和架构集合的信息  
 XML 架构集合在目录视图 sys.xml_schema_collections 中枚举出来。 XML 架构集合“sys”由系统定义。 它包含无需显式加载即可在所有用户定义的 XML 架构集合中使用的预定义命名空间。 此列表包含 xml、xs、xsi、fn 和 xdt 的命名空间。 另外两个目录视图是 sys.xml_schema_namespaces（它枚举每个 XML 架构集合中的所有命名空间）和 sys.xml_components（它枚举每个 XML 架构中的所有 XML 架构组件）。  
  
 内置函数**XML_SCHEMA_NAMESPACE**， *schemaName、 XmlSchemacollectionName、 命名空间 uri*，将生成`xml`数据类型实例... 此实例包含在 XML 架构集合中所包含架构（预定义的 XML 架构除外）的 XML 架构片段。  
  
 可以按下列方式枚举 XML 架构集合的内容：  
  
-   编写对 XML 架构集合的相应目录视图的 Transact-SQL 查询。  
  
-   使用内置函数 **XML_SCHEMA_NAMESPACE()**。 您可以将应用`xml`数据类型方法对此函数的输出。 但不能修改基础 XML 架构。  
  
 这些在下列示例中进行了说明。  
  
### <a name="example-enumerate-the-xml-namespaces-in-an-xml-schema-collection"></a>示例：枚举 XML 架构集合中的 XML 命名空间  
 对 XML 架构集合“myCollection”使用下面的查询：  
  
```  
SELECT XSN.name  
FROM    sys.xml_schema_collections XSC JOIN sys.xml_schema_namespaces XSN  
    ON (XSC.xml_collection_id = XSN.xml_collection_id)  
WHERE    XSC.name = 'myCollection'     
```  
  
### <a name="example-enumerate-the-contents-of-an-xml-schema-collection"></a>示例：枚举 XML 架构集合的内容  
 以下语句枚举关系架构 dbo 中的 XML 架构集合“myCollection”的内容。  
  
```  
SELECT XML_SCHEMA_NAMESPACE (N'dbo', N'myCollection')  
```  
  
 可以为获取集合中的单个 XML 架构`xml`数据类型实例作为第三个参数指定的目标命名空间**xml_schema_namespace （)**。 下面的示例说明了这一点。  
  
### <a name="example-output-a-specified-schema-from-an-xml-schema-collection"></a>示例：从 XML 架构集合输出指定的架构  
 以下语句从关系架构 dbo 中的 XML 架构集合“myCollection”输出目标命名空间为“http://www.microsoft.com/books”的 XML 架构。  
  
```  
SELECT XML_SCHEMA_NAMESPACE (N'dbo', N'myCollection',   
N'http://www.microsoft.com/books')  
```  
  
### <a name="querying-xml-schemas"></a>查询 XML 架构  
 可以按下列方式查询加载到 XML 架构集合的 XML 架构：  
  
-   编写对 XML 架构命名空间的目录视图的 Transact-SQL 查询。  
  
-   创建包含 `xml` 数据类型列的表以存储 XML 架构并将它们加载到 XML 类型系统。 可以通过使用查询 XML 列`xml`数据类型方法。 另外，还可以对此列生成 XML 索引。 但是，使用此方法时，应用程序必须保持 XML 列中存储的 XML 架构和 XML 类型系统之间的一致性。 例如，如果从 XML 类型系统中删除 XML 架构命名空间，还必须从表中删除它以保持一致性。  
  
## <a name="see-also"></a>请参阅  
 [查看存储 XML 架构集合](../xml/view-a-stored-xml-schema-collection.md)   
 [预处理架构以便合并包括的架构](../xml/preprocess-a-schema-to-merge-included-schemas.md)   
 [在服务器上使用 XML 架构集合的要求和限制](../xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
