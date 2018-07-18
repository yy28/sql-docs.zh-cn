---
title: XML 持久性格式 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence format
ms.assetid: 6e146738-ac4d-47bb-b6cd-d87b2260aead
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd0085f4fb632d4e5be4c4e64e1934b154108488
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35273296"
---
# <a name="xml-persistence-format"></a>XML 持久性格式
ADO 使用 utf-8 编码为 XML 流，它仍然存在。  
  
 ADO XML 格式将划分成两个部分后, 跟的数据部分架构部分。 下面是从 Northwind 数据库的 Shippers 表的示例 XML 文件。 下面的示例介绍了各个部分的 XML。  
  
## <a name="remarks"></a>Remarks  
  
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
  
 该架构显示命名空间、 的架构部分中，和的数据部分的声明。 架构部分包含行、 ShipperID、 CompanyName 和 Phone 的定义。  
  
 架构定义符合[W3C XML 数据规范](http://www.w3.org/TR/1998/NOTE-XML-data/)以及是否 （但不会在 Internet Explorer 5） 验证可完全验证。 XML 数据当前是记录集持久性的唯一支持的架构格式。  
  
 数据节中有三个行包含有关货主的信息。 为空的行集，数据部分可能为空，但\<rs： 数据 > 标记必须存在。 没有数据，你可以编写标记速记简单地\<rs： 数据 / >。 前缀为"rs"任何标记指示它是在命名空间中定义的架构 urn:-microsoft-com:rowset。  
  
## <a name="see-also"></a>请参阅  
 [以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)
