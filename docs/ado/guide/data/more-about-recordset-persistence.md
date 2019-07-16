---
title: 有关记录集暂留的详细信息 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: a9b287f5-04b0-4514-8143-f67879ca9842
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bee7d185d5f598a2f0a086bb7e3bea49ddfff88c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924913"
---
# <a name="more-about-recordset-persistence"></a>更多有关记录集暂留的信息
ADO 记录集对象支持存储的内容**记录集**通过使用文件中的对象及其[保存](../../../ado/reference/ado-api/save-method.md)方法。 永久存储的文件可能位于本地驱动器中，服务器或 Web 上的 URL 作为站点。 更高版本，可以使用还原文件[开放](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法**记录集**对象或[Execute](../../../ado/reference/ado-api/execute-method-ado-connection.md)方法[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象。  
  
 此外， [GetString](../../../ado/reference/ado-api/getstring-method-ado.md)方法将**记录集**向窗体中的列和行分隔与你指定的字符的对象。  
  
 若要持久保存**记录集**，首先将其转换为可以存储在文件中的窗体。 **记录集**对象可以存储在专用的高级数据 TableGram (ADTG) 格式或开放的可扩展标记语言 (XML) 格式。 下一节中显示了 ADTG 示例。 有关 XML 暂留的详细信息，请参阅[以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)。  
  
 将任何挂起的更改保存在持久化文件。 执行此操作，可发出一个查询，返回**记录集**对象、 编辑**记录集**，将保存它，并挂起的更改，更高版本将还原**记录集**，，然后更新数据源使用已保存挂起的更改。  
  
 有关持久地存储信息**Stream**对象，请参阅[流和暂留](../../../ado/guide/data/streams-and-persistence.md)。  
  
 有关的示例**记录集**暂留，请参阅 XML 记录集暂留方案。  
  
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
  
 （可选） 如果**记录集**does 不具有的活动连接，您可以接受所有默认设置，以下代码：  
  
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
  
### <a name="open-a-persisted-file-with-rdsdatacontrol"></a>使用 rds。 打开持久化的文件数据控件：  
 在这种情况下， **Server**未设置属性。  
  
```  
Dim dc as New RDS.DataControl  
dc.Connection = "Provider=MSPersist"  
dc.SQL = "c:\yourFile.adtg"  
dc.Refresh  
```  
  
## <a name="see-also"></a>请参阅  
 [GetString 方法 (ADO)](../../../ado/reference/ado-api/getstring-method-ado.md)   
 [Microsoft OLE DB 永久性提供程序 （ADO 服务提供程序）](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [流和暂留](../../../ado/guide/data/streams-and-persistence.md)
