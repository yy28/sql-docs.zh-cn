---
title: 删除数据使用 XML Updategram (SQLXML 4.0) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- <after> block
- updategrams [SQLXML], deleting data
- <before> block
- mapping-schema attribute
- record deletions [SQLXML]
ms.assetid: 4fb116d7-7652-474a-a567-cb475a20765c
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 32134713be17a0770eb58d69529cc34691c181a5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028975"
---
# <a name="deleting-data-using-xml-updategrams-sqlxml-40"></a>使用 XML updategram 删除数据 (SQLXML 4.0)
  Updategram 指示删除操作中的记录实例出现**\<之前 >** 块中没有相应的记录与**\<后 >** 块。 在这种情况下，属的 updategram 删除中的记录**\<之前 >** 从数据库的块。  
  
 下面是 updategram 的删除操作格式：  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema="SampleSchema.xml"]  >  
   <updg:before>  
       <ElementName />  
      [<ElementName .../>... ]  
   </updg:before>  
    [<updg:after>  
    </updg:after>]  
  </updg:sync>  
</ROOT>  
```  
  
 可以省略**\<后 >** 标记如果属的 updategram 正在执行仅删除操作。 如果未指定可选`mapping-schema`属性，  **\<ElementName >** 属的 updategram 映射到数据库表和子元素或属性映射到表中的列中指定。  
  
 如果在属的 updategram 中指定的元素匹配表中的多个行，或不匹配任何行，属的 updategram 返回一个错误，并取消整个**\<同步 >** 块。 updategram 中的元素每次只能删除一个记录。  
  
## <a name="examples"></a>示例  
 本节中的示例使用默认映射（即未在 updategram 中指定映射架构）。 有关使用映射架构的 updategram 的更多示例，请参阅[指定批注映射架构中属的 Updategram &#40;SQLXML 4.0&#41;](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)。  
  
 若要创建使用以下示例的工作示例，必须满足中指定的要求[要求运行 SQLXML 示例](../../sqlxml/requirements-for-running-sqlxml-examples.md)。  
  
### <a name="a-deleting-a-record-by-using-an-updategram"></a>A. 使用 updategram 删除记录  
 以下 updategram 将从 HumanResources.Shift 表中删除两个记录。  
  
 在这些示例中，updategram 不指定映射架构。 因此，updategram 使用默认映射，其中元素名称映射到表名称，而属性或子元素映射到列。  
  
 此第一个属的 updategram 是以属性为中心，在标识 （一天晚上和晚上夜间） 的两个班次**\<之前 >** 块。 因为在没有对应记录**\<后 >** 块，这是一个 delete 操作。  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync >  
  <updg:before>  
       <HumanResources.Shift ShiftID="4"  
                        Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift ShiftID="5"  
                        Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
  </updg:before>  
  <updg:after>  
  </updg:after>  
</updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>测试 updategram  
  
1.  完整示例 （"插入多个记录通过使用属的 updategram"） 中的 B[插入数据使用 XML Updategram &#40;SQLXML 4.0&#41;](inserting-data-using-xml-updategrams-sqlxml-4-0.md)。  
  
2.  将上面 updategram 复制到记事本并将它保存为同一文件夹中的属的 Updategram RemoveShifts.xml，如用来完成 （"插入多个记录通过使用属的 updategram"） 中[插入数据使用 XML Updategram &#40;SQLXML 4.0&#41;](inserting-data-using-xml-updategrams-sqlxml-4-0.md).  
  
3.  创建并使用 SQLXML 4.0 测试脚本 (Sqlxml4test.vbs) 以执行 updategram。  
  
     有关详细信息，请参阅[到执行 SQLXML 4.0 查询使用 ADO](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)。  
  
## <a name="see-also"></a>请参阅  
 [属的 Updategram 安全注意事项&#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  