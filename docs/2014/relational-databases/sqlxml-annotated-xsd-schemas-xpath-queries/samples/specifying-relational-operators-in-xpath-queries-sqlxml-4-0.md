---
title: 在 XPath 查询中指定关系运算符（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], relational operators
- relational operators [SQLXML]
- XPath operators [SQLXML]
- operators [SQLXML]
ms.assetid: 177a0eb2-11ef-4459-a317-485a433ee769
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1597893c203f1223ad916f5c7acecb66ff554c76
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66012442"
---
# <a name="specifying-relational-operators-in-xpath-queries-sqlxml-40"></a>在 XPath 查询中指定关系运算符 (SQLXML 4.0)
  以下示例显示如何在 XPath 查询中指定关系运算符。 这些示例中的 XPath 查询是针对 SampleSchema1.xml 中包含的映射架构指定的。 有关此示例架构的信息，请参阅[&#40;SQLXML 4.0&#41;的 XPath 批注的 XSD 架构示例](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-specify-relational-operator"></a>A. 指定关系运算符  
 此 XPath 查询返回** \<Customer>** 元素的子元素，其中**CustomerID**属性值为 "1"，其中任何子** \<顺序>** 元素包含具有值大于3的**OrderQty**特性的** \<OrderDetail>** 子元素：  
  
```  
/child::Customer[@CustomerID="1"]/Order/OrderDetail[@OrderQty > 3]  
```  
  
 方括号中指定的谓词用于筛选** \<Customer>** 元素。 仅返回** \<客户>** 元素，这些元素至少具有一个** \<OrderDetail**为 OrderQty 特性值大于3的>孙。  
  
 
  `child` 轴为默认轴。 因此，可以将该查询指定为：  
  
```  
/Customer[@CustomerID="1"]/Order/OrderDetail[@OrderQty > 3]  
```  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>针对映射架构测试 XPath 查询  
  
1.  复制[示例架构代码](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)，并将其粘贴到文本文件中。 将该文件另存为 SampleSchema1.xml。  
  
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
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
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
 此查询将返回**SalesPersonID**属性值小于270的上下文节点>元素子级的所有** \<顺序**：  
  
```  
/child::Customer/child::Order[(attribute::SalesPersonID < 270)=true()]  
```  
  
 可以指定 `attribute` 轴 (@) 的快捷方式，由于 `child` 轴是默认值，因此可以在查询中省略它：  
  
```  
/Customer/Order[(@SalesPersonID < 270)=true()]  
```  
  
> [!NOTE]  
>  在模板中指定该查询时，必须对 < 字符进行实体编码，因为 < 字符在 XML 文档中具有特殊含义。 在模板中，使用`<`指定 < 字符。  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>针对映射架构测试 XPath 查询  
  
1.  复制[示例架构代码](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)，并将其粘贴到文本文件中。 将该文件另存为 SampleSchema1.xml。  
  
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
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
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
  
  
