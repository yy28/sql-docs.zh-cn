---
title: 数据部分 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data section [ADO]
ms.assetid: 43dc42a8-7057-48e6-93d6-880d5c5c51a4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6a06b2291d07378b63907b4a195fa3902930078
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472544"
---
# <a name="data-section"></a>数据部分
数据部分定义以及任何挂起的更新、 插入或删除的行集的数据。 数据部分可以包含零个或多个行。 它只能包含一个行集，其中行定义的架构中的数据。 此外，如前面提到的则可以省略列不包含任何数据。 如果某个属性或子元素使用的 data 节中，并且未在架构部分中定义该构造，则以无提示方式将其忽略。  
  
## <a name="string"></a>String  
 XML 文本数据中的保留的字符必须替换为合适的字符实体。 例如，在公司名称"Joe 的车库"中单引号必须替换由一个实体。 实际行将如下所示：  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 以下字符是保留在 XML 中，并且必须替换为字符实体: {，"，&，\<，>}。  
  
## <a name="binary"></a>二进制  
 二进制数据是用编码 （即，一个字节映射到两个字符、 每半个字节的一个字符）。  
  
## <a name="datetime"></a>DateTime  
 XML 数据的数据类型不直接支持变体的 VT_DATE 格式。 日期使用的数据和时间组件的正确格式是 yyyy-mm-ddThh:mm:ss。  
  
 有关指定的 XML 的日期格式的详细信息，请参阅[W3C XML 数据规范](https://go.microsoft.com/fwlink/?LinkId=5692)。  
  
 如果 XML 数据规范定义两个等效数据类型 (例如，i4 = = int)，ADO 将写出的友好名称，但在这种读取。  
  
## <a name="managing-pending-changes"></a>管理挂起的更改  
 可以在立即打开记录集或批更新模式。 当为客户端游标的批处理更新模式中打开时，对记录集所做的所有更改都处于挂起状态 UpdateBatch 方法调用之前。 挂起的更改也将永久保存时保存记录集。 在 XML 中，它们表示通过使用 urn： 架构中定义的"更新"元素-microsoft-com:rowset。 此外，如果可以更新行集，可更新的属性必须设置为 true 的行的定义中。 例如，若要定义运货商表包含挂起的更改、 行定义将外观类似于以下。  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 这将告知到图面上的数据持久性提供程序，以便 ADO 可以构建一个可更新的记录集对象。  
  
 下面的示例数据显示了插入操作、 更改和删除操作在持久化文件中的查找如何。  
  
```  
<rs:data>  
  <z:row ShipperID="2" CompanyName="United Package"   
    Phone="(503) 555-3199"/>  
<rs:update>  
  <rs:original>  
    <z:row ShipperID="3" CompanyName="Federal Shipping"   
      Phone="(503) 555-9931"/>  
  </rs:original>  
  <z:row Phone="(503) 552-7134"/>  
</rs:update>  
<rs:insert>  
  <z:row ShipperID="12" CompanyName="Lightning Shipping"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="13" CompanyName="Thunder Overnight"   
    Phone="(505) 111-2222"/>  
  <z:row ShipperID="14" CompanyName="Blue Angel Air Delivery"   
    Phone="(505) 111-2222"/>  
</rs:insert>  
<rs:delete>  
  <z:row ShipperID="1" CompanyName="Speedy Express" Phone="(503) 555-9831"/>  
</rs:delete>  
</rs:data>  
```  
  
 更新始终包含已更改的行数据应遵循的整个原始行数据。 已更改的行可能包含的所有列或实际发生了更改这些列。 在上一示例中，发运方 2 的行不会更改，并且只有电话列已发运方 3 更改值，因此已更改的行中包含的唯一列。 运货商 12、 13 和 14 的插入的行是批处理一起在一个 rs： 插入标记。 尽管上一示例中未显示这一点，请注意在一起，还可以成批删除的行。  
  
## <a name="see-also"></a>请参阅  
 [以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)
