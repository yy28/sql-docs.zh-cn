---
title: 架构部分 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Schema section [ADO]
ms.assetid: 4ac6e524-2c92-48e8-b871-0a4b5c8fda18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45e8e37d8bb85e727771072abda9249b8155076f
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2019
ms.locfileid: "54256192"
---
# <a name="schema-section"></a>架构部分
架构部分是必需的。 如前面的示例所示，ADO 写出详细的元数据有关的每个列以保留尽可能多地用于更新的数据值的语义信息。 但是，若要在 XML 中加载，ADO 仅需要列和到其所属的行集的名称。 下面是最小架构的示例：  
  
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
  
 在上一示例中，ADO 将数据视为可变长度字符串因为无类型信息包含在架构中。  
  
## <a name="creating-aliases-for-column-names"></a>为列名创建别名  
 使用 rs: name 属性，可创建列名称的别名，以便在行集的列信息中显示的友好名称可能和可能的 data 节中使用较短的名称。 例如，可以修改以前的架构，将 ShipperID 映射到 s1 到 s2，CompanyName Phone 到 s3，如下所示：  
  
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
  
 然后，在数据部分中，该行将使用 name 属性 （不 rs： 名称） 来引用该列：  
  
```  
"<row s1="1" s2="Speedy Express" s3="(503) 555-9831"/>  
```  
  
 为列名创建别名是必需的只要列名称不是有效的特性或 XML 中的标记名称。 例如，"LastName"必须含有一个别名因为具有嵌入的空格的名称无效的特性。 下面的行不会正确处理被 XML 分析器中，因此必须创建不具有嵌入的空格的其他名称的别名。  
  
```  
<row last name="Jones"/>  
```  
  
 必须在 XML 文档的架构和数据部分中引用该列的每个位置一致地使用 name 属性使用的任何值。 下面的示例显示了使用一致的 s1:  
  
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
  
 同样，因为没有任何别名为定义`CompanyName`在上一示例中，`CompanyName`必须文档中一致地使用。  
  
## <a name="data-types"></a>数据类型  
 可以将数据类型应用到含 dt: type 属性的列。 允许的 XML 类型的权威指南，请参阅的数据类型部分[W3C XML 数据规范](http://www.w3.org/TR/1998/NOTE-XML-data/)。 可以通过两种方式指定数据类型： 直接在列定义本身上指定 dt: type 特性或使用 s:datatype 构造作为列定义的嵌套元素。 例如，  
  
```  
<s:AttributeType name="Phone" >  
  <s:datatype dt:type="string"/>  
</s:AttributeType>  
```  
  
 等效于  
  
```  
<s:AttributeType name="Phone" dt:type="string"/>  
```  
  
 如果您 dt: type 中完全省略属性行定义中，默认情况下，列的类型将可变长度的字符串。  
  
 如果有比只是类型名称 (例如，dt: maxlength) 的更多类型信息时，它可以更具可读性，若要使用 s:datatype 子元素。 这是只是一个约定，但是，并不是要求。  
  
 以下示例进一步演示如何在您的架构中包含的类型信息。  
  
```  
<!-- 1. String with no max length -->  
<s:AttributeType name="title_id"/>  
<!-or -->  
<s:AttributeType name="title_id" dt:type="string"/>  
  
<!-- 2. Fixed length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" rs:fixedlength="true" />  
</s:AttributeType>  
  
<!-- 3. Variable length string with max length of 6 -->  
<s:AttributeType name="title_id">  
    <s:datatype dt:type="string" dt:maxLength="6" />  
</s:AttributeType>  
  
<!-- 4. Integer -->  
<s:AttributeType name="title_id" dt:type="int"/>  
```  
  
 没有使用细微的第二个示例中的 rs: fixedlength 属性。 使用 rs: fixedlength 属性的列设置为真，则数据必须包含在架构中定义的长度。 在这种情况下，title_id 的有效值是"123456，"按原样"123"。 但是，"123"不会有效因为其长度为 3，而非 6。 请参阅 OLE DB 程序员指南更完整的 fixedlength 属性的说明。  
  
## <a name="handling-nulls"></a>处理 null 值  
 通过 rs: maybenull 属性处理 null 值。 如果此属性设置为 true，列的内容可以包含 null 值。 此外，如果行数据中找不到列，返回的行集读取数据的用户将从 IRowset::GetData() 获取 null 状态。 请考虑以下运货商表中的列定义。  
  
```  
<s:AttributeType name="ShipperID">  
  <s:datatype dt:type="int" dt:maxLength="4"/>  
</s:AttributeType>  
<s:AttributeType name="CompanyName">  
  <s:datatype dt:type="string" dt:maxLength="40" rs:maybenull="true"/>  
</s:AttributeType>  
```  
  
 定义允许`CompanyName`应为空，但`ShipperID`不能包含 null 值。 如果数据部分包含以下行，永久性提供程序将设置为数据的状态`CompanyName`到 OLE DB 状态常量 DBSTATUS_S_ISNULL 列：  
  
```  
<z:row ShipperID="1"/>  
```  
  
 如果行是完全为空，按如下所示，永久性提供程序将返回为 DBSTATUS_E_UNAVAILABLE 的 OLE DB 状态`ShipperID`和 CompanyName 的 DBSTATUS_S_ISNULL。  
  
```  
<z:row/>   
```  
  
 请注意，长度为零的字符串不相同，则为 null。  
  
```  
<z:row ShipperID="1" CompanyName=""/>  
```  
  
 对于前面的行，永久性提供程序将返回这两个列 DBSTATUS_S_OK 的 OLE DB 状态。 `CompanyName`只需在这种情况下是""（长度为零的字符串）。  
  
 构造可用于 OLE DB 中的 XML 文档架构使用 OLE DB 的详细信息，请参阅的定义"urn： 架构-microsoft-com:rowset"和 OLE DB 程序员指南。  
  
## <a name="see-also"></a>请参阅  
 [以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)
