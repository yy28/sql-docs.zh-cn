---
title: "在 XPath 查询 (SQLXML 4.0) 中指定关系运算符 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], relational operators
- relational operators [SQLXML]
- XPath operators [SQLXML]
- operators [SQLXML]
ms.assetid: 177a0eb2-11ef-4459-a317-485a433ee769
caps.latest.revision: "25"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 02c8a5c597bf49af0837af5ad229c709b11dc570
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="specifying-relational-operators-in-xpath-queries-sqlxml-40"></a>在 XPath 查询中指定关系运算符 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]下面的示例演示如何关系运算符在 XPath 查询中指定。 这些示例中的 XPath 查询是针对 SampleSchema1.xml 中包含的映射架构指定的。 有关此示例架构的信息，请参阅[示例批注 XSD 架构 XPath 示例 &#40;SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md).  
  
## <a name="examples"></a>示例  
  
### <a name="a-specify-relational-operator"></a>A. 指定关系运算符  
 此 XPath 查询返回的子元素的**\<客户 >**元素其中**CustomerID**属性值是"1"和其中任何子**\<顺序>**元素包含 **\<OrderDetail >**具有子项**OrderQty**具有大于 3 的值属性：  
  
```  
/child::Customer[@CustomerID="1"]/Order/OrderDetail[@OrderQty > 3]  
```  
  
 方括号筛选器中指定的谓词**\<客户 >**元素。 仅**\<客户 >**至少有一个元素 **\<OrderDetail >**孙具有大于 3 返回 OrderQty 属性值。  
  
 **子**轴是默认设置。 因此，可以将该查询指定为：  
  
```  
/Customer[@CustomerID="1"]/Order/OrderDetail[@OrderQty > 3]  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>针对映射架构测试 XPath 查询  
  
1.  复制[示例架构代码](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)并将其粘贴到文本文件。 将该文件另存为 SampleSchema1.xml。  
  
2.  创建以下模板 (SpecifyRelationalA.xml)，并将它保存在保存 SampleSchema1.xml 的目录中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer[@CustomerID="1"]/Order/OrderDetail[@OrderQty > 3]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     为映射架构 (SampleSchema1.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[到执行 SQLXML 4.0 查询使用 ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 下面是执行该模板的结果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <OrderDetail ProductID="Prod-760" UnitPrice="503.3507" OrderQty="4" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-763" UnitPrice="503.3507" OrderQty="4" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-766" UnitPrice="503.3507" OrderQty="4" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-732" UnitPrice="440.1742" OrderQty="4" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-757" UnitPrice="1049.7528" OrderQty="4" UnitPriceDiscount="0" />   
</ROOT>  
```  
  
### <a name="b-specify-relational-operator-in-the-xpath-query-and-use-boolean-function-to-compare-the-result"></a>B. 在 XPath 查询中指定关系运算符并使用布尔函数比较该结果  
 此查询返回所有**\<顺序 >**的上下文节点的具有元素子级， **SalesPersonID**属性为小于 270 的值：  
  
```  
/child::Customer/child::Order[(attribute::SalesPersonID < 270)=true()]  
```  
  
 快捷方式**属性**轴 (@) 可指定，而是因为**子**轴默认值时，它可以在查询中省略：  
  
```  
/Customer/Order[(@SalesPersonID < 270)=true()]  
```  
  
> [!NOTE]  
>  在模板中指定该查询时，< 字符必须进行实体编码，因为 < 字符在 XML 文档中有特殊含义。 在模板中，请使用 `<` 指定 < 字符。  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>针对映射架构测试 XPath 查询  
  
1.  复制[示例架构代码](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/samples/sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)并将其粘贴到文本文件。 将该文件另存为 SampleSchema1.xml。  
  
2.  创建以下模板 (SpecifyRelationalB.xml)，并将它保存在保存 SampleSchema1.xml 的目录中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="SampleSchema1.xml">  
            /Customer/Order[(@SalesPersonID<270)=true()]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     为映射架构 (SampleSchema1.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[到执行 SQLXML 4.0 查询使用 ADO](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
 下面是执行该模板的部分结果集：  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="Ord-46613" SalesPersonID="268"   
         OrderDate="2002-07-01T00:00:00"   
         DueDate="2002-07-13T00:00:00"   
         ShipDate="2002-07-08T00:00:00">  
    <OrderDetail ProductID="Prod-739" UnitPrice="917.9363"   
                 OrderQty="2" UnitPriceDiscount="0" />   
    <OrderDetail ProductID="Prod-779" UnitPrice="1491.4221"   
                 OrderQty="1" UnitPriceDiscount="0" />   
    <OrderDetail ProductID="Prod-825" UnitPrice="242.1391"   
                 OrderQty="1" UnitPriceDiscount="0" />   
  </Order>  
  <Order SalesOrderID="Ord-71919" SalesPersonID="268"  
         OrderDate="2004-06-01T00:00:00"   
         DueDate="2004-06-13T00:00:00"   
         ShipDate="2004-06-08T00:00:00">  
    <OrderDetail ProductID="Prod-961" UnitPrice="534.492"   
                 OrderQty="1" UnitPriceDiscount="0" />   
    <OrderDetail ProductID="Prod-965" UnitPrice="534.492"   
                 OrderQty="1" UnitPriceDiscount="0" />   
    <OrderDetail ProductID="Prod-966" UnitPrice="1716.5304"   
                 OrderQty="1" UnitPriceDiscount="0" />   
  </Order>  
  ...  
</ROOT>  
```  
  
  
