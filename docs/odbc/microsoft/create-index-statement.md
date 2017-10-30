---
title: "创建索引语句 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0f6e7525059640e7ffdadd79ec26a62229eabae9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="create-index-statement"></a>创建索引语句
CREATE INDEX 语句的语法是：  
  
 创建 [UNIQUE] 索引*索引名称*ON*表名*(*列标识符*[ASC] [DESC] [，*列标识符*[ASC][DESC]...])与\<*索引选项列表*>  
  
 其中\<*索引选项列表*> 可以是： 主 &#124;不允许 NULL &#124;忽略 NULL  
  
 仅 Microsoft Access 驱动程序使用不允许 NULL 和 NULL 忽略索引选项。 DBASE 和 Paradox 驱动程序接受语法，但请忽略的任一选项的存在。  
  
 当使用 Paradox 驱动程序时，CREATE INDEX 语句创建 Paradox 主密钥文件和次要文件。  
  
 此语句不支持的 Microsoft Excel 或文本的驱动程序。

