---
title: 创建索引语句 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6aa512ff789fcbd00f45f84fb194d4ab3f5da07
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280967"
---
# <a name="create-index-statement"></a>CREATE INDEX 语句
CREATE INDEX 语句的语法是：  
  
 在*表名*上创建 [唯一]*索引名称*（*列标识符*[ASC][DESC]，*列标识符*[ASC][DESC]...）带\<*索引选项列表*>  
  
 \<*索引选项列表*>可以是：主&#124;无效 &#124;忽略 NULL  
  
 只有 Microsoft Access 驱动程序使用"无效"和"忽略"空索引选项。 dBASE 和 Paradox 驱动程序接受语法，但忽略任一选项的存在。  
  
 使用悖论驱动程序时，CREATE INDEX 语句将创建 Paradox 主键文件和辅助文件。  
  
 Microsoft Excel 或文本驱动程序不支持此语句。
