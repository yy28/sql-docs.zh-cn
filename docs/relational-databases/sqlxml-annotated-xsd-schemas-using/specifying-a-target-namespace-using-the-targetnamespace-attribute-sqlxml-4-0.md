---
title: 使用指定目标 Namespace targetNamespace 属性 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- namespaces [SQLXML], annotated XSD schemas
- targetNamespace attribute
- XSD schemas [SQLXML], target namespaces
- annotated XSD schemas, target namespaces
- xsd:targetNamespace
- attributeFormDefault attribute
- elementFormDefault attribute
- target namespaces [SQLXML]
ms.assetid: f3df9877-6672-4444-8245-2670063c9310
author: MightyPen
ms.author: genemi
ms.reviewer: ''
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a52ce206eee69fa585a72788e46f8f7174d936a8
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2019
ms.locfileid: "65980819"
---
# <a name="specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-40"></a>使用 targetNamespace 属性指定目标命名空间 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  编写 XSD 架构，您可以使用 XSD **targetNamespace**特性以指定目标命名空间。 本主题介绍如何在 XSD **targetNamespace**， **elementFormDefault**，并**attributeFormDefault**属性起作用，它们如何影响的 XML 实例生成，以及如何使用命名空间指定 XPath 查询。  
  
 可以使用**xsd: targetnamespace**属性元素和默认命名空间的属性放入不同的命名空间。 还可以指定在显示局部声明的架构元素和属性时，是否应由命名空间限定（使用前缀显式限定或默认隐式限定）。 可以使用**elementFormDefault**并**attributeFormDefault**上的特性 **\<xsd: schema >** 元素，以便全局指定可以使用的局部元素和特性，或您限定**窗体**属性分别指定各个元素和属性。  
  
## <a name="examples"></a>示例  
 若要创建使用以下示例的工作示例，必须满足某些要求。 有关详细信息，请参阅[运行 SQLXML 示例的要求](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-specifying-a-target-namespace"></a>A. 指定目标命名空间  
 通过使用以下 XSD 架构指定的目标命名空间**xsd: targetnamespace**属性。 架构还设置**elementFormDefault**并**attributeFormDefault**属性值为 **"unqualified"** （这些属性的默认值）。 这是全局声明，并会影响所有局部元素 (**\<顺序 >** 架构中) 和属性 (**CustomerID**， **ContactName**，和**OrderID**架构中)。  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
            xmlns:CO="urn:MyNamespace"   
            targetNamespace="urn:MyNamespace" >  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer"   
               sql:relation="Sales.Customer"   
               type="CO:CustomerType" />  
  
  <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                     sql:relationship="CustOrders"  
                     type="CO:OrderType" />  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
        <xsd:attribute name="SalesPersonID"  type="xsd:string" />  
  </xsd:complexType>  
  <xsd:complexType name="OrderType" >  
     <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
     <xsd:attribute name="CustomerID" type="xsd:string" />  
  </xsd:complexType>  
</xsd:schema>  
```  
  
 在架构中：  
  
-   **CustomerType**并**OrderType**类型声明是全局的并且因此，包含在该架构的目标命名空间。 因此，当被引用这些类型的声明中**\<客户 >** 元素并将其**\<顺序 >** 子元素，这就关联指定前缀目标命名空间。  
  
-   **\<客户 >** 元素也包含在架构的目标命名空间，因为它是在架构中的全局元素。  
  
 针对该架构执行以下 XPath 查询：  
  
```  
(/CO:Customer[@CustomerID=1)   
```  
  
 该 XPath 查询生成以下实例文档（仅显示了一部分订单）：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <y0:Customer xmlns:y0="urn:MyNamespace"   
      CustomerID="ALFKI" ContactName="Maria Anders">  
        <Order CustomerID="ALFKI" OrderID="10643" />   
        <Order CustomerID="ALFKI" OrderID="10692" />   
        ...  
  </y0:Customer>  
  </ROOT>  
```  
  
 以下实例文档定义 urn: MyNamespace 命名空间，并将关联到它的前缀 (y0)。 前缀仅适用于**\<客户 >** 全局元素。 (该元素是全局的因为它被声明为的子 **\<xsd: schema >** 架构中的元素。)  
  
 前缀不应用于局部元素和属性，因为值**elementFormDefault**并**attributeFormDefault**属性设置为 **"unqualified"** 架构中。 请注意， **\<顺序 >** 是局部元素，因为其声明显示为的子 **\<complexType >** 元素，用于定义 **\<CustomerType >** 元素。 同样，属性 (**CustomerID**， **OrderID**，并**ContactName**) 本地，而非全局。  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>创建此架构的工作示例  
  
1.  复制上面的架构代码，并将它粘贴到文本文件中。 将文件另存为 targetNameSpace.xml。  
  
2.  复制以下模板，并将它粘贴到文本文件中。 在保存 targetNamespace.xml 的目录中将该文件另存为 targetNameSpaceT.xml。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="targetNamespace.xml"  
                       xmlns:CO="urn:MyNamespace" >  
        /CO:Customer[@CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     在模板中的 XPath 查询返回**\<客户 >** CustomerID 为 1 的客户的元素。 请注意，XPath 查询为查询中的元素（而不是属性）指定命名空间前缀。 （根据架构中的指定，未限定局部属性。）  
  
     为映射架构 (targetNamespace.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\MyDir\targetNamepsace.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 查询](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 如果架构指定了**elementFormDefault**并**attributeFormDefault**属性的值 **"qualified"**，实例文档将具有所有本地限定元素和属性。 可以更改以前的架构，将在这些属性包括 **\<xsd: schema >** 元素，然后重新执行该模板。 由于当前在实例中也限定了这些属性，XPath 查询将改为包括命名空间前缀。  
  
 下面是修改后的 XPath 查询：  
  
```  
/CO:Customer[@CO:CustomerID=1]  
```  
  
 下面是返回的 XML 文档：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
   <y0:Customer xmlns:y0="urn:MyNamespace" CustomerID="1" SalesPersonID="280">  
      <Order SalesOrderID="43860" CustomerID="1" />   
      <Order SalesOrderID="44501" CustomerID="1" />   
      <Order SalesOrderID="45283" CustomerID="1" />   
      <Order SalesOrderID="46042" CustomerID="1" />   
   </y0:Customer>  
</ROOT>  
```  
  
  
