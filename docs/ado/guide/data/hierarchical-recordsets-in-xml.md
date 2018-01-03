---
title: "在 XML 中的分层记录集 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: hierarchical Recordsets [ADO], in XML
ms.assetid: 5d4b11c4-c94f-4910-b99b-5b9abc50d791
caps.latest.revision: "4"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9916333a203309d81228c86c019277c9d5515313
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="hierarchical-recordsets-in-xml"></a>在 XML 中的分层记录集
ADO 允许持久性的分层记录集对象转换为 XML。 与层次结构的记录集对象中父记录集的值是字段的另一个记录集。 此类字段将呈现为 XML 流，而不是属性的子元素。  
  
## <a name="remarks"></a>Remarks  
 下面的示例演示这种情况下：  
  
```  
Rs.Open "SHAPE {select stor_id, stor_name, state from stores} APPEND ({select stor_id, ord_num, ord_date, qty from sales} AS rsSales RELATE stor_id TO stor_id)", "Provider=MSDataShape;DSN=pubs;Integrated Security=SSPI;"  
```  
  
 下面是持久化的记录集的 XML 格式：  
  
```  
<xml xmlns:s="uuid:BDC6E3F0-6DA3-11d1-A2A3-00AA00C14882"     xmlns:dt="uuid:C2F41010-65B3-11d1-A29F-00AA00C14882"     xmlns:rs="urn:schemas-microsoft-com:rowset"   
    xmlns:z="#RowsetSchema">   
  <s:Schema id="RowsetSchema">   
    <s:ElementType name="row" content="eltOnly" rs:updatable="true">   
      <s:AttributeType name="stor_id" rs:number="1"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="4"   
          rs:fixedlength="true" rs:maybenull="false"/>   
      </s:AttributeType>   
      <s:AttributeType name="stor_name" rs:number="2" rs:nullable="true"   
        rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="40"/>   
      </s:AttributeType>   
      <s:AttributeType name="state" rs:number="3" rs:nullable="true"   
        rs:writeunknown="true">   
        <s:datatype dt:type="string" dt:maxLength="2"   
          rs:fixedlength="true"/>   
      </s:AttributeType>   
      <s:ElementType name="rsSales" content="eltOnly"   
        rs:updatable="true" rs:relation="010000000100000000000000">   
        <s:AttributeType name="stor_id" rs:number="1"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="4"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_num" rs:number="2"   
          rs:writeunknown="true">   
          <s:datatype dt:type="string" dt:maxLength="20"   
            rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="ord_date" rs:number="3"   
          rs:writeunknown="true">   
            <s:datatype dt:type="dateTime" dt:maxLength="16"   
              rs:scale="3" rs:precision="23" rs:fixedlength="true"   
              rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:AttributeType name="qty" rs:number="4" rs:writeunknown="true">   
          <s:datatype dt:type="i2" dt:maxLength="2" rs:precision="5"   
            rs:fixedlength="true" rs:maybenull="false"/>   
        </s:AttributeType>   
        <s:extends type="rs:rowbase"/>   
      </s:ElementType>   
      <s:extends type="rs:rowbase"/>   
    </s:ElementType>   
  </s:Schema>   
  <rs:data>   
    <z:row stor_id="6380" stor_name="Eric the Read Books" state="WA">   
      <rsSales stor_id="6380" ord_num="6871"   
        ord_date="1994-09-14T00:00:00" qty="5"/>   
      <rsSales stor_id="6380" ord_num="722a"   
        ord_date="1994-09-13T00:00:00" qty="3"/>   
    </z:row>   
    <z:row stor_id="7066" stor_name="Barnum's" state="CA">   
      <rsSales stor_id="7066" ord_num="A2976"   
        ord_date="1993-05-24T00:00:00" qty="50"/>   
      <rsSales stor_id="7066" ord_num="QA7442.3"   
        ord_date="1994-09-13T00:00:00" qty="75"/>   
    </z:row>   
    <z:row stor_id="7067" stor_name="News & Brews" state="CA">   
      <rsSales stor_id="7067" ord_num="D4482"   
        ord_date="1994-09-14T00:00:00" qty="10"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="40"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
      <rsSales stor_id="7067" ord_num="P2121"   
        ord_date="1992-06-15T00:00:00" qty="20"/>   
    </z:row>   
  </rs:data>   
</xml>   
```  
  
 如果以这种方式保持不变，记录集的父代中的列的确切顺序不明显。 父代中的任何字段可能包含子记录集。 永久性提供程序出第一次为属性的所有标量列仍然存在，然后作为子元素的父行保存出所有子记录集"列"。 字段的序号位置的父代中可以通过查看该记录集的架构定义获取记录集。 每个字段均包含该字段的序号的记录集架构命名空间中定义的 OLE DB 属性 rs： 数。  
  
 中子记录集的所有字段的名称都串联在一起，其中包含此子记录集的父代中字段的名称。 这是为了确保在其中父级和子级这两个记录集包含来自两个不同的表，但又单独命名的字段的情况下没有名称冲突。  
  
 将层次结构的记录集保存为 XML 时，你应注意的 ADO 中的以下限制：  
  
-   无法将记录与层次结构集挂起的更新保存到 XML。  
  
-   不能使用参数化的形状命令创建分层记录集保留 （采用 XML 或 ADTG 格式）。  
  
-   ADO 当前将父和子记录集之间的关系保存为二进制大型对象 (BLOB)。 XML 标记来描述此关系具有尚未定义行集架构命名空间中。  
  
-   保存分层的记录集后，所有子记录集与一起都保存它。 如果当前的记录集是另一个记录集的子级，则不会保存其父级。 保存所有子窗体的当前记录集的子树的记录集。  
  
 当分层的记录集重新打开从其保留在 XML 的格式，你必须注意以下限制：  
  
-   如果子记录包含有没有相应的父记录的记录，这些行不会写出分层记录集的 XML 表达形式。 因此，从其持久化的位置打开记录集时，这些行，将会丢失。  
  
-   如果子记录具有到多个父记录的引用，然后在重新打开记录集，子记录集可能包含重复的记录。 但是，这些重复项只能是如果用户可直接与基础的子行集可见。 如果某章节用于导航子记录集 （这是在 ADO 中导航的唯一方法），则重复项不可见。  
  
## <a name="see-also"></a>另请参阅  
 [以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)
