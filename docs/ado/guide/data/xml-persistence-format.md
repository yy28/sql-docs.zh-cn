---
title: XML 暂留格式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence format
ms.assetid: 6e146738-ac4d-47bb-b6cd-d87b2260aead
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2330703450e42e8ddf9bfeed536dd3649d65edf8
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2019
ms.locfileid: "54255682"
---
# <a name="xml-persistence-format"></a>XML 暂留格式
ADO 使用 utf-8 编码的 XML 流，它仍然存在。  
  
 ADO XML 格式将划分成两个部分后, 跟数据部分的架构部分。 以下是 Northwind 数据库中的运货商表的示例 XML 文件。 下面的示例介绍了各个部分的 XML。  
  
## <a name="remarks"></a>备注  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"   
xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"   
xmlns:rs="urn:schemas-microsoft-com:rowset"   
xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="ShipperID" rs:number="1"   
        rs:basetable="shippers" rs:basecolumn="ShipperID"  
        rs:keycolumn="true">   
        <s:datatype dt:type="int" dt:maxLength="4" rs:precision="10"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="CompanyName" rs:number="2"   
        rs:nullable="true" rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="CompanyName">   
        <s:datatype dt:type="string" dt:maxLength="40" />   
      </s:AttributeType>   
      <s:AttributeType name="Phone" rs:number="3" rs:nullable="true"   
        rs:write="true" rs:basetable="shippers"   
        rs:basecolumn="Phone">   
        <s:datatype dt:type="string" dt:maxLength="24"/>   
      </s:AttributeType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  
  <rs:data>   
    <z:row ShipperID="1" CompanyName="Speedy Express"   
      Phone="(503) 555-9831"/>   
    <z:row ShipperID="2" CompanyName="United Package"   
      Phone="(503) 555-3199"/>   
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>   
  </rs:data>   
</xml>  
```  
  
 架构演示了命名空间、 架构部分和数据部分的声明。 架构部分包含行、 ShipperID、 CompanyName 和 Phone 的定义。  
  
 架构定义符合[W3C XML 数据规范](http://www.w3.org/TR/1998/NOTE-XML-data/)（尽管在 Internet Explorer 5 中将不进行验证） 可以完全验证。 XML 数据当前是记录集暂留的唯一支持的架构格式。  
  
 数据节中有三个行包含运货商有关的信息。 对于空的行集，数据部分可能为空，但\<rs： 数据 > 标记必须存在。 不包含数据，您可以编写标记速记简单地\<rs： 数据 / >。 前缀为"rs"任何标记指示它是由 urn： 架构定义的命名空间中的 microsoft-com:rowset。  
  
## <a name="see-also"></a>请参阅  
 [以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)
