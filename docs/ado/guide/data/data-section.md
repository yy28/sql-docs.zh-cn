---
title: "数据部分 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data section [ADO]
ms.assetid: 43dc42a8-7057-48e6-93d6-880d5c5c51a4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 62eb026fac4588cc159afec1714a6aa51903aa8a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="data-section"></a>数据部分
数据部分定义以及任何挂起的更新、 插入或删除的行集的数据。 数据节可以包含零个或多个行。 它只能包含一个行集，其中行定义的架构中的数据。 此外，如前面提到的那样，可以忽略不包含任何数据的列。 如果某个属性或子元素使用的数据部分中，并且未在架构部分中定义该构造，则以无提示方式忽略它。  
  
## <a name="string"></a>字符串  
 文本数据中的 XML 保留的字符必须替换为相应的字符实体。 例如，在公司名称"Joe 的车库"中单引号必须替换由一个实体。 实际行将如下所示：  
  
```  
<z:row CompanyName="Joe's Garage"/>  
```  
  
 以下的字符是保留在 XML 中，并且必须替换字符实体为: {，"，&，\<，>}。  
  
## <a name="binary"></a>二进制  
 二进制数据是 bin.hex 编码 （即，一个字节映射到两个字符、 每半个字节的一个字符）。  
  
## <a name="datetime"></a>DateTime  
 XML 数据的数据类型不直接支持 variant VT_DATE 格式。 与的数据和时间的组件的日期的正确格式是 yyyy-mm-ddThh:mm:ss。  
  
 有关通过 XML 指定的日期格式的详细信息，请参阅[W3C XML 数据规范](https://go.microsoft.com/fwlink/?LinkId=5692)。  
  
 当 XML 数据规范定义了两个等效的数据类型 (例如，i4 = = int)，ADO 将写出的友好名称，但在这两中读取。  
  
## <a name="managing-pending-changes"></a>管理挂起的更改  
 可以在即时中打开记录集或批处理更新模式。 当在与客户端游标的批处理更新模式下打开它们时，对记录集所做的所有更改都处于挂起状态直到调用 UpdateBatch 方法。 挂起的更改也将永久保存保存记录集时。 在 XML 中，它们表示通过使用 urn： 架构中定义的"更新"元素-microsoft-com:rowset。 此外，如果可以更新行集，可更新的属性必须设置为 true 的行定义中。 例如，若要定义 Shippers 表包含挂起的更改、 将行定义外观类似于以下。  
  
```  
<s:ElementType name="row" content="eltOnly" updatable="true">  
  <s:attribute type="ShipperID"/>  
  <s:attribute type="CompanyName"/>  
  <s:attribute type="Phone"/>  
  <s:extends type="rs:rowbase"/>  
</s:ElementType>  
```  
  
 这将告知曲面数据到永久性提供程序，以便 ADO 可以构建可更新的记录集对象。  
  
 下面的示例数据显示如何插入、 更改和删除在持久化文件中。  
  
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
  
 更新始终包含已更改的行数据应遵循的整个原始行数据。 已更改的行可能包含的所有列或已实际更改的那些列。 在前面的示例中，发货方 2 的行不会更改，并且只有电话列已发货方 3 更改值，因此已更改的行中包含的唯一列。 货主 12、 13 和 14 插入的行是批处理组合在一起的下一个 rs： 插入标记。 尽管这不会显示在前面的示例，请注意，也可一起成批已删除的行。  
  
## <a name="see-also"></a>另请参阅  
 [保留记录采用 XML 格式](../../../ado/guide/data/persisting-records-in-xml-format.md)
