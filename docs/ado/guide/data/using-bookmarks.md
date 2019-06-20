---
title: 使用书签 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- bookmarks [ADO]
- Recordset object [ADO]
ms.assetid: cca244e6-84f8-4394-bca9-f7a819b8f4df
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c7e14e063d1aabcfce6391a85c0fcddbf0ff4e9f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704614"
---
# <a name="using-bookmarks"></a>使用书签
通常很有用处： 返回后需要移动中直接与特定记录**记录集**而无需滚动浏览每个记录和比较值。 例如，如果你尝试搜索记录使用**查找**方法，但搜索未返回任何记录，系统会自动在的任何一端**记录集**。 如果您的提供程序支持它们，可以使用书签来标记在使用之前的位置**查找**方法，以便你可以返回到你的位置。 书签是**Variant**键入值，该值唯一地标识中的记录**记录集**对象。  
  
 此外可以使用与书签的变体数组**记录集筛选器**方法对所选的一组记录进行筛选。 有关此技术的详细信息，请参阅主题中的结果进行筛选[使用记录集](../../../ado/guide/data/working-with-recordsets.md)，在本部分中更高版本。  
  
 可以使用**书签**属性，书签获得一条记录，或者在中设置的当前记录**记录集**标识的有效书签记录的对象。 下面的代码使用**书签**属性来设置书签，然后转到其他记录之后返回到用书签标记的记录。 若要确定你**记录集**支持书签，使用**支持**方法。  
  
```  
'BeginBookmarkEg  
Dim varBookmark As Variant  
Dim blnCanBkmrk As Boolean  
  
objRs.Open strSQL, strConnStr, adOpenStatic, adLockOptimistic, adCmdText  
  
If objRs.RecordCount > 4 Then  
    objRs.Move 4                       ' move to the fifth record  
    blnCanBkmrk = objRs.Supports(adBookmark)  
    If blnCanBkmrk = True Then  
        varBookmark = objRs.Bookmark   ' record the bookmark  
        objRs.MoveLast                 ' move to a different record  
        objRs.Bookmark = varBookmark   ' return to the bookmarked (sixth) record  
    End If  
End If  
'EndBookmarkEg  
```  
  
 [支持](../../../ado/reference/ado-api/supports-method.md)更高版本中更详细地介绍方法。  
  
 除了克隆**记录集**，唯一的书签将变为**记录集**在其中创建了它们，即使使用相同的命令。 这意味着，不能使用**书签**获取从一个**记录集**若要在一秒内移动到同一条记录**记录集**使用相同的命令打开。
