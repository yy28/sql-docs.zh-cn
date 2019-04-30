---
title: XPath 查询 (SQLXML 4.0) 中指定布尔运算符 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XPath operators [SQLXML]
- OR operator
- Boolean operators
- XPath queries [SQLXML], Boolean operators
- operators [SQLXML]
ms.assetid: 9928cff5-62ac-42aa-96bf-2e09a1df0bc3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ae0350a239414b4e20299cf42d46ebc5b9a69023
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273360"
---
# <a name="specifying-boolean-operators-in-xpath-queries-sqlxml-40"></a>在 XPath 查询中指定布尔运算符 (SQLXML 4.0)
  以下示例说明如何在 XPath 查询中指定布尔运算符。 本示例中的 XPath 查询针对 SampleSchema1.xml 中包含的映射架构指定。 有关该示例架构的信息，请参阅[示例带批注的 XSD 架构的 XPath 示例&#40;SQLXML 4.0&#41;](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-specify-the-or-boolean-operator"></a>A. 指定 OR 布尔运算符  
 此 XPath 查询将返回**\<客户 >** 的上下文节点的子元素**CustomerID**属性值为 13 或 31:  
  
```  
/child::Customer[attribute::CustomerID="13" or attribute::CustomerID="31"]  
```  
  
 可以指定指向 `attribute` 轴 (@) 的快捷方式，并且，由于 `child` 轴是默认的，因此可以忽略它：  
  
```  
/Customer[@CustomerID="13" or @CustomerID="31"]  
```  
  
 在谓词中，`attribute`是轴和`CustomerID`是节点测试 (如果**CustomerID**是**\<属性 >** 节点，因为 **\<属性 >** 节点是主节点`attribute`轴)。 谓词筛选器**\<客户 >** 元素并返回只有满足条件的谓词中指定。  
  
##### <a name="to-test-the-xpath-queries-against-the-mapping-schema"></a>若要测试针对映射架构的 XPath 查询  
  
1.  复制[示例架构代码](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)并将其粘贴到文本文件中。 将该文件另存为 SampleSchema1.xml。  
  
2.  创建以下模板 (BooleanOperatorsA.xml) 并将其保存到保存 SampleSchema1.xml 的目录中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /Customer[@CustomerID="13" or @CustomerID="31"]  
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
  <Customer CustomerID="13" SalesPersonID="286" TerritoryID="7" AccountNumber="13" CustomerType="S" />   
  <Customer CustomerID="31" SalesPersonID="286" TerritoryID="7" AccountNumber="31" CustomerType="S" Orders="Ord-51803 Ord-69427">  
    <Order SalesOrderID="Ord-51803" SalesPersonID="286" OrderDate="2003-08-01T00:00:00" DueDate="2003-08-13T00:00:00" ShipDate="2003-08-08T00:00:00">  
      <OrderDetail ProductID="Prod-718" UnitPrice="1059.31" OrderQty="1" UnitPriceDiscount="0" />   
      <OrderDetail ProductID="Prod-838" UnitPrice="1059.31" OrderQty="1" UnitPriceDiscount="0" />   
    </Order>  
    <Order SalesOrderID="Ord-69427" SalesPersonID="286" OrderDate="2004-05-01T00:00:00" DueDate="2004-05-13T00:00:00" ShipDate="2004-05-08T00:00:00">  
      <OrderDetail ProductID="Prod-835" UnitPrice="440.1742" OrderQty="1" UnitPriceDiscount="0" />   
    </Order>  
  </Customer>  
</ROOT>  
```  
  
  
