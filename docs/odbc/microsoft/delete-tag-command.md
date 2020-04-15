---
title: 删除 TAG 命令 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97ca5abca7e70f5dffdae9bf14ce64429fd203d5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303538"
---
# <a name="delete-tag-command"></a>DELETE TAG 命令
从复合索引 （.cdx） 文件中删除标记或标记。  
  
## <a name="syntax"></a>语法  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>参数  
 *标签名称1**CDXFilename1*[，*标签名称2* *[CDXFilename2]...*  
 指定要从复合索引文件中删除的标记。 您可以通过包含用逗号分隔的标记名称列表来删除具有一个 DELETE TAG 的多个标记。 如果打开索引文件中存在两个或多个同名标记，则可以通过包括 OF *CDXFileName*来从特定索引文件中删除标记。  
  
 所有 *[CDX 文件名 ]*  
 从复合索引文件中删除每个标记。 如果当前表具有结构复合索引文件，则从索引文件中删除所有标记，从磁盘中删除索引文件，删除表标头中指示存在关联结构复合索引文件的标志。 将 ALL 与 OF *CDXFileName*一起使用，从打开的复合索引文件中删除结构复合索引文件以外的所有标记。  
  
## <a name="remarks"></a>备注  
 使用 INDEX 创建的复合索引文件包含与索引条目对应的标记。 删除标签用于从打开的复合索引文件中删除标记或标记。 您只能从当前工作区中打开的复合索引文件中删除标记。 如果从复合索引文件中删除所有标记，则该文件将从磁盘中删除。  
  
 Visual FoxPro 首先查找结构复合索引文件中的标记（如果一个已打开）。 如果标记不在结构复合索引文件中，Visual FoxPro 然后在其他打开的复合索引文件中查找标记。  
  
## <a name="see-also"></a>另请参阅  
 [INDEX 命令](../../odbc/microsoft/index-command.md)
