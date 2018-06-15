---
title: 显式映射 XSD 元素和属性表和列 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- explicit schema mapping [SQLXML]
- XPath queries [SQLXML], annotated XSD schemas in queries
- sql:field
- row mapping [SQLXML]
- attribute mapping [SQLXML], explicit mapping
- field annotation
- XSD schemas [SQLXML], mapping attributes and elements
- names [SQLXML]
- relation annotation
- table/view mapping [SQLXML], explicit mapping
- sql:relation
- mapping schema [SQLXML], explicit mapping
- annotated XSD schemas, mapping attributes and elements
- column mapping [SQLXML]
- element mapping [SQLXML], explicit mapping
- table mapping [SQLXML], explicit mapping
- element/attribute mapping [SQLXML]
ms.assetid: 7a5ebeb6-7322-4141-a307-ebcf95976146
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1836db12438017023637185d6e8ba24a6e533a77
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32970614"
---
# <a name="explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns"></a>显式映射 XSD 元素和属性表和列
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  当使用 XSD 架构提供关系数据库的 XML 视图时，必须将该架构的元素和属性映射至数据库的表和列。 数据库表/视图中的行将映射至 XML 文档中的元素。 数据库中的列值映射到属性或元素。  
  
 当针对带批注的 XSD 架构指定 XPath 查询时，将从该架构中的元素和属性的数据映射到的表和列中检索这些数据。 若要从数据库中获取单个值，XSD 架构中指定的映射必须同时具备关系和字段规范。 如果元素/属性的名称不是它映射到的表/视图或列名称与同名**sql:relation**和**sql:field**使用批注来指定元素之间的映射或在 XML 文档和表 （视图） 或数据库中的列的属性。  
  
## <a name="sql-relation"></a>sql-relation  
 **Sql:relation**添加批注，以将 XSD 架构中的 XML 节点映射到数据库表。 表 （视图） 的名称指定的值为**sql:relation**批注。  
  
 当**sql:relation**指定在元素上，此批注的作用域适用于所有属性和该元素，因此提供中编写的快捷方式的复杂类型定义中所述的子元素批注。  
  
 **Sql:relation**批注也是有用时在中有效的标识符是[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 XML 中无效。 例如，“Order Details”是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的有效表名，但该名称在 XML 中无效。 在这种情况下， **sql:relation**批注可以用于指定映射，例如：  
  
```  
<xsd:element name="OD" sql:relation="[Order Details]">  
```  
  
## <a name="sql-field"></a>sql-field  
 **Sql 字段**批注将元素或属性映射到数据库列。 **Sql:field**添加批注，以将架构中的 XML 节点映射到的数据库列。 不能指定**sql:field**上空内容元素。  
  
## <a name="examples"></a>示例  
 若要创建使用以下示例的工作示例，必须满足某些要求。 有关详细信息，请参阅[要求运行 SQLXML 示例](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-the-sqlrelation-and-sqlfield-annotations"></a>A. 指定 sql:relation 和 sql:field 批注  
 此示例中，在 XSD 架构组成**\<联系人 >** 包含复杂类型的元素 **\<FName >** 和 **\<LName >** 子元素和**ContactID**属性。  
  
 **Sql:relation**批注地图**\<联系人 >** 到 Person.Contact 表 AdventureWorks 数据库中的元素。 **Sql:field**批注地图 **\<FName >** 到 FirstName 列的元素和 **\<LName >** LastName 的元素列。  
  
 为指定任何批注**ContactID**属性。 这导致将属性默认映射为具有相同名称的列。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Contact" sql:relation="Person.Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"  
                     sql:field="FirstName"   
                     type="xsd:string" />   
        <xsd:element name="LName"    
                     sql:field="LastName"    
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ContactID"   
                       type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>若要测试示例 XPath 查询根据架构  
  
1.  复制上面的架构代码，并将它粘贴到文本文件中。 将文件另存为 MySchema-annotated.xml。  
  
2.  复制下面的模板，然后将其粘贴到文本文件中。 在您保存 MySchema-annotated.xml 的相同目录中将该文件另存为 MySchema-annotatedT.xml。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="MySchema-annotated.xml">  
        /Contact  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     为映射架构 (MySchema-annotated.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\SqlXmlTest\MySchema-annotated.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[到执行 SQLXML 查询使用 ADO](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 下面是部分结果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
 <Contact ContactID="1">   
    <FName>Gustavo</FName>   
    <LName>Achong</LName>   
 </Contact>   
  .....  
</ROOT>  
```  
  
  
