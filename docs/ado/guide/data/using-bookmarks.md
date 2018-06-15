---
title: 使用书签 |Microsoft 文档
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
- bookmarks [ADO]
- Recordset object [ADO]
ms.assetid: cca244e6-84f8-4394-bca9-f7a819b8f4df
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 643d07d49e2e2ec0e31f9a677796f309fedd0d1d
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35273216"
---
# <a name="using-bookmarks"></a>使用书签
通常很有用，在需要移动中后返回到特定记录直接**记录集**而无需滚动的每个记录，并比较值。 例如，如果你尝试搜索记录使用**查找**方法，但搜索未返回任何记录，系统会自动在的任何一端**记录集**。 如果你的提供商支持它们，可以使用书签来将你的位置标记在使用之前**查找**方法，以便你可以返回到你的位置。 书签是**Variant**键入值，该值唯一地标识中的记录**记录集**对象。  
  
 你还可以使用的书签的 variant 数组**记录集筛选器**方法要作为筛选依据一组选定的记录。 有关此技术的详细信息，请参阅筛选在主题中，结果[处理记录集](../../../ado/guide/data/working-with-recordsets.md)，本部分中更高版本。  
  
 你可以使用**书签**属性书签对于记录，在获取或设置当前记录**记录集**到由有效的书签记录的对象。 下面的代码使用**书签**属性来设置书签，然后在上移到其他记录后返回到标有书签的记录。 若要确定你**记录集**支持书签，使用**支持**方法。  
  
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
  
 [支持](../../../ado/reference/ado-api/supports-method.md)方法更高版本更详细地介绍。  
  
 除了克隆**记录集**，唯一的书签将变为**记录集**在其中创建了它们，即使使用相同的命令。 这意味着，不能使用**书签**从一个获取**记录集**一秒钟内将移到同一记录**记录集**使用相同的命令打开。
