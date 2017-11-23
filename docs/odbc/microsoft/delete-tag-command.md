---
title: "删除标记命令 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: DELETE TAG command [ODBC]
ms.assetid: 4f4e1362-a5f3-4b15-8a3c-d4e96605f221
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5e31cf41163f512b5450e5452f8e0adff5c0a604
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="delete-tag-command"></a>删除标记命令
从复合索引 (.cdx) 文件中删除一个标记。  
  
## <a name="syntax"></a>语法  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>参数  
 *TagName1*的*CDXFileName1*[， *TagName2*[OF *CDXFileName2*]]...  
 指定一个标记可从复合索引文件中删除。 你可以通过包括用逗号分隔的标记名称的列表删除具有一个删除标记的多个标记。 如果在打开索引文件中存在具有相同名称的两个或多个标记，则可以通过包括的从特定索引文件删除标记*CDXFileName*。  
  
 所有 [OF *CDXFileName*]  
 从复合索引文件中删除每个标记。 如果当前表具有结构的复合索引文件，所有标记都会从索引文件、 从磁盘中，删除该索引文件和都删除表的标头，该值指示存在相关联的结构化复合索引文件中的标志。 所有用于 OF *CDXFileName*若要从非结构化的复合索引文件打开复合索引文件中删除所有标记。  
  
## <a name="remarks"></a>注释  
 复合索引文件，使用索引创建，包含对应于索引条目的标记。 删除标记用于从打开的复合索引文件中删除一个标记。 从当前工作区中打开的复合索引文件，可以删除仅标记。 如果从复合索引文件中删除所有标记，将从磁盘中删除该文件。  
  
 Visual FoxPro 会首先中查找的结构化的复合索引文件中的标记 （如果打开）。 如果标记不在结构化的复合索引文件，Visual FoxPro 然后查找其他打开的复合索引文件中的标记。  
  
## <a name="see-also"></a>另请参阅  
 [INDEX 命令](../../odbc/microsoft/index-command.md)
