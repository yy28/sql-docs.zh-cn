---
title: 从 XML 文档中使用 sql 中排除架构元素： 映射 |Microsoft 文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- element does not map [SQLXML]
- annotated XSD schemas, excluding schema elements
- mapped annotation
- table mapping [SQLXML], excluding schema elements
- sql:mapped
- excluding schema elements
- element mapping [SQLXML], excluding schema elements
- column mapping [SQLXML]
- XSD schemas [SQLXML], excluding schema elements
- attribute mapping [SQLXML], excluding schema elements
- table/view mapping [SQLXML], excluding schema elements
ms.assetid: 7d2649dd-0038-4a2c-b16d-f80f7c306966
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 640ae49de50fec55afb9c957042f5d317f41195f
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38001239"
---
# <a name="excluding-schema-elements-from-the-xml-document-using-sqlmapped"></a>从 XML 文档中使用 sql 中排除架构元素： 映射
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  由于是默认映射，XSD 架构中的每个元素和属性都映射到数据库表/视图和列。 如果你想要不映射到任何数据库表 （视图） 或列并且，未出现在 XML 中的 XSD 架构中创建的元素，可以指定**sql： 映射**批注。  
  
 **Sql： 映射**批注是特别有用，如果不能修改架构或如果使用的架构验证 XML 从其他源和尚未包含未存储在数据库中的数据。 **Sql： 映射**批注不同于**sql： 是常量**，因为未映射的元素和属性不出现在 XML 文档。  
  
 **Sql： 映射**批注接受布尔值 (0 = false,1 = true)。 可接受的值为 0、1、true 和 false。  
  
## <a name="examples"></a>示例  
 若要创建使用以下示例的工作示例，必须满足某些要求。 有关详细信息，请参阅[运行 SQLXML 示例的要求](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-the-sqlmapped-annotation"></a>A. 指定 sql:mapped 批注  
 假定您有来自其他源的 XSD 架构。 此 XSD 架构组成 **\<Person.Contact >** 具有元素**ContactID**， **FirstName**， **LastName**，和**HomeAddress**属性。  
  
 在将此 XSD 架构映射到 AdventureWorks 数据库中的 Person.Contact 表**sql： 映射**上指定**HomeAddress**属性，因为 Employees 表不存储主页雇员的地址。 因此，在针对映射架构指定 XPath 查询时，此属性不会映射到数据库，并且不会在生成的 XML 文档中返回此属性。  
  
 为架构的其余部分进行默认映射。 **\<Person.Contact >** 元素映射到 Person.Contact 表中，而所有属性都映射到 Person.Contact 表中的相同名称的列。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Person.Contact">  
    <xsd:complexType>  
      <xsd:attribute name="ContactID"   type="xsd:string"/>  
      <xsd:attribute name="FirstName"    type="xsd:string" />  
      <xsd:attribute name="LastName"     type="xsd:string" />  
      <xsd:attribute name="HomeAddress" type="xsd:string"   
                     sql:mapped="false" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>若要测试示例 XPath 查询根据架构  
  
1.  复制上面的架构代码，并将它粘贴到文本文件中。 将文件另存为 sql-mapped.xml。  
  
2.  复制以下模板，并将它粘贴到文本文件中。 在保存 sql-mapped.xml 的相同目录中将该文件另存为 sql-mappedT.xml。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sql-mapped.xml">  
            /Person.Contact[@ContactID < 10]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     为映射架构 (MySchema.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\MyDir\sql-mapped.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 查询](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 下面是结果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact ContactID="1" FirstName="Gustavo" LastName="Achong" />   
  <Person.Contact ContactID="2" FirstName="Catherine" LastName="Abel" />   
  <Person.Contact ContactID="3" FirstName="Kim" LastName="Abercrombie" />   
  <Person.Contact ContactID="4" FirstName="Humberto" LastName="Acevedo" />   
  <Person.Contact ContactID="5" FirstName="Pilar" LastName="Ackerman" />   
  <Person.Contact ContactID="6" FirstName="Frances" LastName="Adams" />   
  <Person.Contact ContactID="7" FirstName="Margaret" LastName="Smith" />   
  <Person.Contact ContactID="8" FirstName="Carla" LastName="Adams" />   
  <Person.Contact ContactID="9" FirstName="Jay" LastName="Adams" />   
</ROOT>  
```  
  
 请注意，ContactID、 FirstName 和 LastName 都存在，但 HomeAddress 是不是因为映射架构指定了值为 0 **sql： 映射**属性。  
  
## <a name="see-also"></a>请参阅  
 [XSD 元素和属性到表和列的默认映射&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
  
  
