---
title: DELETE TAG 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE TAG command [ODBC]
ms.assetid: 4f4e1362-a5f3-4b15-8a3c-d4e96605f221
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eabecbc399751f03e9e5c25b32423ce0839072dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63198247"
---
# <a name="delete-tag-command"></a>DELETE TAG 命令
从复合索引 (.cdx) 文件中删除标记。  
  
## <a name="syntax"></a>语法  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>参数  
 *TagName1*OF *CDXFileName1*[, *TagName2*[OF *CDXFileName2*]] ...  
 指定一个标记，以从复合索引文件中删除。 可以通过包括一系列以逗号分隔的标记名称与一个删除标记删除多个标记。 如果在打开索引文件中存在具有相同名称的两个或多个标记，则可以通过包含的从特定索引文件删除标记*CDXFileName*。  
  
 ALL [OF *CDXFileName*]  
 从复合索引文件中删除每个标记。 如果当前表具有结构复合索引文件，从索引文件中删除所有标记、 从磁盘中，将删除该索引文件和都删除表的标头，该值指示存在相关联的结构化复合索引文件中的标志。 使用所有这些都有 OF *CDXFileName*若要从非结构化的复合索引文件打开复合索引文件删除所有标记。  
  
## <a name="remarks"></a>备注  
 复合索引文件，使用索引，创建包含对应于索引项的标记。 删除标记用于从打开的复合索引文件中删除标记。 可以从当前工作区中打开的复合索引文件删除仅标记。 如果从复合索引文件中删除所有标记，该文件是从磁盘中删除。  
  
 Visual FoxPro 会首先中查找结构化的复合索引文件中的标记 （如果打开）。 如果标记不在结构化的复合索引文件，Visual FoxPro 然后寻找其他打开的复合索引文件中的标记。  
  
## <a name="see-also"></a>请参阅  
 [INDEX 命令](../../odbc/microsoft/index-command.md)
