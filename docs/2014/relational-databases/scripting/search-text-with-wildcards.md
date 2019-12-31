---
title: 使用通配符搜索文本
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- vswildcardsbuilder
helpviewer_keywords:
- searches [SQL Server Management Studio], wildcards
- Query Editor [SQL Server Management Studio], wildcard searches
- wildcard options [SQL Server Management Studio]
ms.assetid: 449600f8-cc87-4b3f-878a-59c158a88a40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caeda52d612f4df6672f686e06834de6fef0cc67
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243279"
---
# <a name="search-text-with-wildcards"></a>使用通配符搜索文本
  以下表达式可以替换 " [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **查找和替换**" 对话框的 "**查找内容**" 字段中的字符或数字。  
  
#### <a name="to-search-using-wildcards"></a>使用通配符进行搜索  
  
1.  若要在“快速查找”、 **“在文件中查找”** 、 **“快速替换”** 或 **“在文件中替换”** 操作过程中在 **“查找内容”** 字段中使用通配符，请选择 **“查找选项”** 下的 **“使用”** 选项，然后选择 **“通配符”**。  
  
2.  
  **“查找内容”** 字段旁边的 **“引用列表”** 三角形按钮将变为可用状态。 单击此按钮以显示可用通配符列表。 从 **“引用列表”** 中选择任意项后，便会将该项插入到 **“查找内容”** 字符串中。  
  
 下表介绍了 **“引用列表”** 中可用的通配符。  
  
|表达式|语法|说明|  
|----------------|------------|-----------------|  
|任何单个字符|?|与任何单个字符匹配。|  
|任何单个数字|#|与任何单个数字匹配。 例如，7# 与包括 7 且其后跟随另一数字的数字匹配，例如 71，但不能是 17。|  
|集合中没有的字符|[! ]|与未在集合中指定的任一字符匹配。|  
|一个或多个字符|*|与任何一个或多个字符匹配。 例如，new* 与任何包括“new”的文本匹配，例如 newfile.txt。|  
|字符集|[ ]|与在集合中指定的任一字符匹配。|  
  
## <a name="see-also"></a>另请参阅  
 [搜索和替换](search-and-replace.md)   
 [用正则表达式搜索文本](search-text-with-regular-expressions.md)  
