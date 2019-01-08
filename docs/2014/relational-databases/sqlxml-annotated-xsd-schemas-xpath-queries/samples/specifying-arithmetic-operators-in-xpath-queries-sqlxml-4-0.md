---
title: 在 XPath 查询 (SQLXML 4.0) 中指定算数运算符 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- arithmetic operators
- XPath operators [SQLXML]
- XPath queries [SQLXML], arithmetic operators
- operators [SQLXML]
ms.assetid: fdfbc87d-759f-4abc-acf5-a21de01f78d3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4ab35bbdac79f9c6f9835d50db376b0b19227217
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52807239"
---
# <a name="specifying-arithmetic-operators-in-xpath-queries-sqlxml-40"></a>在 XPath 查询中指定算数运算符 (SQLXML 4.0)
  以下示例说明如何在 XPath 查询中指定算数运算符。 本示例中的 XPath 查询针对 SampleSchema1.xml 中包含的映射架构指定。 有关该示例架构的信息，请参阅[示例带批注的 XSD 架构的 XPath 示例&#40;SQLXML 4.0&#41;](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-specify-the--arithmetic-operator"></a>A. 指定 * 算数运算符  
 此 XPath 查询将返回 **\<OrderDetail >** 满足指定的谓词的元素：  
  
```  
/child::OrderDetail[@UnitPrice * @Quantity = 12.350]  
```  
  
 在查询中，`child`是轴和`OrderDetail`是节点测试 (如果**OrderDetail**是**\<元素节点 >**，因为 **\<元素 >** 节点是主节点`child`轴)。 为所有 **\<OrderDetail >** 元素节点，在谓词中的测试应用，并返回满足条件的这些节点。  
  
> [!NOTE]  
>  XPath 中的数字是双精度浮点数，对本示例中的浮点数进行比较将导致舍入。  
  
##### <a name="to-test-the-xpath-query-against-the-mapping-schema"></a>针对映射架构测试 XPath 查询  
  
1.  复制[示例架构代码](sample-annotated-xsd-schema-for-xpath-examples-sqlxml-4-0.md)并将其粘贴到文本文件中。 将该文件另存为 SampleSchema1.xml。  
  
2.  创建以下模板 (ArithmeticOperatorA.xml)，并将它保存在保存 SampleSchema1.xml 的目录中。  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="SampleSchema1.xml">  
        /OrderDetail[@UnitPrice * @OrderQty = 12.350]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     为映射架构 (SampleSchema1.xml) 指定的目录路径是相对于模板保存目录的相对路径。 也可以指定绝对路径，例如：  
  
    ```  
    mapping-schema="C:\MyDir\SampleSchema1.xml"  
    ```  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 执行该模板。  
  
     有关详细信息，请参阅[使用 ADO 执行 SQLXML 4.0 查询](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
```  
Here is the partial result set of the template execution:    
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-709" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
  <OrderDetail ProductID="Prod-710" UnitPrice="6.175" OrderQty="2" UnitPriceDiscount="0" />   
   ...  
</ROOT>  
```  
  
  
