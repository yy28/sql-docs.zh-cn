---
title: 有关记录集持久性的详细信息 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: a9b287f5-04b0-4514-8143-f67879ca9842
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11bceb2bdeeced8ddbe98e7ddc1164e216644264
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="more-about-recordset-persistence"></a>有关记录集持久性的详细信息
ADO 记录集对象支持存储内容**记录集**通过使用文件中的对象及其[保存](../../../ado/reference/ado-api/save-method.md)方法。 永久存储的文件可能存在位于本地驱动器中，服务器，或在网站上的 URL 为站点。 更高版本，可以还原该文件使用[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法**记录集**对象或[执行](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
 此外， [GetString](../../../ado/reference/ado-api/getstring-method-ado.md)方法将**记录集**到窗体中的列和行分隔与你指定的字符的对象。  
  
 若要保留**记录集**，首先将其转换为可以存储在文件中的窗体。 **记录集**对象可以存储在专用的高级数据表图 (ADTG) 格式或打开的可扩展标记语言 (XML) 格式。 在下一部分中演示了 ADTG 示例。 有关 XML 持久性的详细信息，请参阅[保留的记录，采用 XML 格式](../../../ado/guide/data/persisting-records-in-xml-format.md)。  
  
 保存到持久化文件中的任何挂起的更改。 这样，您可以发出查询返回**记录集**对象、 编辑**记录集**、 将它和挂起的更改保存、 更高版本还原**记录集**，，然后更新数据源与保存挂起的更改。  
  
 有关永久存储信息**流**对象，请参阅[流和持久性](../../../ado/guide/data/streams-and-persistence.md)。  
  
 有关的示例**记录集**持久性，请参阅 XML 记录集持久化方案。  
  
## <a name="example"></a>示例  
  
### <a name="save-a-recordset"></a>保存记录集：  
  
```  
Dim rs as New ADODB.Recordset  
rs.Save "c:\yourFile.adtg", adPersistADTG  
```  
  
### <a name="open-a-persisted-file-with-recordsetopen"></a>打开具有 Recordset.Open 持久化的文件：  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg", "Provider=MSPersist",,,adCmdFile  
```  
  
 （可选） 如果**记录集**未没有活动连接，你可以接受所有默认值，下面的代码：  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "c:\yourFile.adtg"  
```  
  
### <a name="open-a-persisted-file-with-connectionexecute"></a>打开具有 Connection.Execute 持久化的文件：  
  
```  
Dim conn as New ADODB.Connection  
Dim rs as ADODB.Recordset  
conn.Open "Provider=MSPersist"  
Set rs = conn.execute("c:\yourFile.adtg")  
```  
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>使用 rds.打开持久化的文件DataControl:  
 在这种情况下，**服务器**未设置属性。  
  
```  
Dim dc as New RDS.DataControl  
dc.Connection = "Provider=MSPersist"  
dc.SQL = "c:\yourFile.adtg"  
dc.Refresh  
```  
  
## <a name="see-also"></a>另请参阅  
 [GetString 方法 (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)   
 [Microsoft OLE DB 永久性提供程序 （ADO 服务提供程序）](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [流和暂留](../../../ado/guide/data/streams-and-persistence.md)
