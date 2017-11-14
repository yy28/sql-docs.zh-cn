---
title: "架构部分 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Schema section [ADO]
ms.assetid: 4ac6e524-2c92-48e8-b871-0a4b5c8fda18
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3f691a4ba9632f40ceb4eb08c33a35135d9a0e7d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="schema-section"></a>架构部分
架构部分是必需的。 如前面的示例所示，ADO 写出详细的元数据有关每一列来保留的数据值语义尽可能多地更新。 但是，若要在 XML 中加载，ADO 仅需要的列和它们所属的行集的名称。 下面是架构的最小的示例：  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"  
    xmlns:rs="urn:schemas-microsoft-com:rowset"  
    xmlns:z="#RowsetSchema">  
  <s:Schema id="RowsetSchema">  
    <s:ElementType name="row" content="eltOnly">  
      <s:AttributeType name="ShipperID"/>  
      <s:AttributeType name="CompanyName"/>  
      <s:AttributeType name="Phone"/>  
      <s:Extends type="rs:rowbase"/>  
    </s:ElementType>  
  </s:Schema>  
  <rs:data>  
...  
  </rs:data>  
</xml>  
```  
  
 在前面的示例中，ADO 将数据视为可变长度字符串因为无类型信息包含在架构中。  
  
## <a name="creating-aliases-for-column-names"></a>为列名称创建别名  
 Rs: name 属性，可创建一个列名称的别名，以便友好名称可能出现在行集公开的列信息，并可能在数据部分中使用较短的名称。 例如，无法修改上面的架构，以将 ShipperID 映射到 s1、 s2、 到 CompanyName 和电话到 s3，如下所示：  
  
```  
<s:Schema id="RowsetSchema">   
<s:ElementType name="row" content="eltOnly" rs:updatable="true">   
<s:AttributeType name="s1" rs:name="ShipperID" rs:number="1" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s2" rs:name="CompanyName" rs:number="2" ...>   
...  
</s:AttributeType>   
<s:AttributeType name="s3" rs:name="Phone" rs:number="3" ...>   
...  
</s:AttributeType>   
...  
</s:ElementType>   
</s:Schema>  
```  
  
 然后，在数据部分中，该行将使用 （不 rs： 名称） 中的名称属性来引用该列：  
  
```  
"<row s1="1" s2="Speedy Express" s3="(503) 555-9831"/>  
```  
  
 创建对列名称的别名是必需的只要一个列名称不是有效的特性或在 XML 中的标记名称。 例如，"LastName"必须具有别名因为具有嵌入的空格的名称是无效的属性。 下面的行不会正确处理 XML 分析器中，因此你必须创建不具有嵌入的空格的一些其他名称的别名。  
  
```  
<row last name="Jones"/>  
```  
  
 在每个位置的 XML 文档的架构和数据部分中引用的列必须一致地使用名称属性使用任何值。 下面的示例演示 s1 一致地使用：  
  
```  
<s:Schema id="RowsetSchema">  
  <s:ElementType name="row" content="eltOnly">  
    <s:attribute type="s1"/>  
    <s:attribute type="CompanyName"/>  
    <s:attribute type="s3"/>  
    <s:extends type="rs:rowbase"/>  
  </s:ElementType>  
  <s:AttributeType name="s1" rs:name="ShipperID" rs:number="1"   
    rs:maydefer="true" rs:writeunknown="true">  
    <s:datatype dt:type="i4" dt:maxLength="4" rs:precision="10"   
      rs:fixedlength="true" rs:maybenull="true"/>  
  </s:AttributeType>  
</s:Schema>  
<rs:data>  
  <z:row s1="1" CompanyName="Speedy Express" s3="(503) 555-9831"/>  
</rs:data>  
```  
  
 同样，因为没有定义任何别名为`CompanyName`在前面的示例中，`CompanyName`必须使用在整个文档的一致。  
  
## <a name="data-types"></a>数据类型  
 你可以应用到具有 dt: type 属性的列数据类型。 允许的 XML 类型的权威指南，请参阅的数据类型部分[W3C XML 数据规范](http://www.w3.org/TR/1998/NOTE-XML-data/)。 你可以通过两种方式指定数据类型： 直接在列定义本身上指定 dt: type 属性或 s:datatype 构造用作列定义的嵌套元素。 例如：  
  
```  
<s:AttributeType name="Phone" >  
  <s:datatype dt:type="string"/>  
</s:AttributeType>  
```  
  
 等效于  
  
```  
<s:AttributeType name="Phone" dt:type="string"/>  
```  
  
 如果省略完全从行定义中，dt: type 属性默认情况下，列的类型将是可变长度的字符串。  
  
 如果你具有比仅仅是类型名称 (例如，dt: maxlength) 的多个类型信息，它使更具可读性，若要使用 s:datatype 子元素。 这是仅使用约定，但是和不是必需。  
  
 下面的示例进一步显示如何在您的架构中包括类型信息。  
  
```  
<!-- 1. String with no max length -->  
<s:AttributeType name="title_id"/>  
<!—or -->  
<s:AttributeType name="title_id" dt:type="string"/>  
  
<!—- 2. Fixed length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" rs:fixedlength="true" />  
</s:AttributeType>  
  
<!—- 3. Variable length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" />  
</s:AttributeType>  
  
<!—- 4. Integer -->  
<s:AttributeType name="title_id" dt:type="int"/>  
```  
  
 没有使用细微的第二个示例中的 rs: fixedlength 属性。 Rs: fixedlength 属性具有的列设置为 true 则意味着数据必须具有的架构中定义的长度。 在这种情况下，title_id 的有效值是"123456、"按原样"123"。 但是，"123"将不能因为其长度为 3，而非 6。 请参阅 OLE DB 程序员指南更 fixedlength 属性的完整说明。  
  
## <a name="handling-nulls"></a>处理 null 值  
 由 rs: maybenull 属性处理 null 值。 如果此属性设置为 true，列的内容可以包含 null 值。 此外，如果行数据中找不到列，返回从行集中读取的数据的用户将从 IRowset::GetData() 获取 null 状态。 请考虑货主表中的以下列定义。  
  
```  
<s:AttributeType name="ShipperID">  
  <s:datatype dt:type="int" dt:maxLength="4"/>  
</s:AttributeType>  
<s:AttributeType name="CompanyName">  
  <s:datatype dt:type="string" dt:maxLength="40" rs:maybenull="true"/>  
</s:AttributeType>  
```  
  
 定义允许`CompanyName`为 null，但`ShipperID`不能包含 null 值。 如果数据部分包含以下行，永久性提供程序会将设置的数据的状态`CompanyName`到 OLE DB 状态常量是 DBSTATUS_S_ISNULL 列：  
  
```  
<z:row ShipperID="1"/>  
```  
  
 如果行，如下所示完全为空，，永久性提供程序将返回有关 DBSTATUS_E_UNAVAILABLE 的 OLE DB 状态`ShipperID`和 CompanyName 的是 DBSTATUS_S_ISNULL。  
  
```  
<z:row/>   
```  
  
 请注意零长度字符串不是 null 相同。  
  
```  
<z:row ShipperID="1" CompanyName=""/>  
```  
  
 对于前面的行，永久性提供程序将返回两个列 DBSTATUS_S_OK 的 OLE DB 状态。 `CompanyName`在这种情况下只是""（零长度字符串）。  
  
 有关 OLE DB 的进一步信息构造可用于 OLE DB 在 XML 文档的架构中使用，请参阅的定义"urn： 架构-microsoft-com:rowset"和 OLE DB 程序员指南。  
  
## <a name="see-also"></a>另请参阅  
 [保留记录采用 XML 格式](../../../ado/guide/data/persisting-records-in-xml-format.md)

