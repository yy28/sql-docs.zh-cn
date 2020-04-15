---
title: 外部联接转义序列 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- outer join escape sequence [ODBC]
- escape sequences [ODBC], outer join
- ODBC escape sequences [ODBC], outer join
ms.assetid: 2cfd1525-6677-4d36-9b9e-730496853750
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37ce446328d263f492cdfd369f6e8f9f64fe6dfc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303608"
---
# <a name="outer-join-escape-sequence"></a>外部联接转义序列
ODBC 使用外部联接的转义序列。 此转义序列的语法如下：  
  
```  
{oj outer-join}  
```  
  
## <a name="remarks"></a>备注  
 在 BNF 符号中，语法如下所示：  
  
 *ODBC-外部联接转义*：：*  
  
 *ODBC-esc-开始器*oj*外部联接 ODBC-esc 终结器*  
  
 *外部联接*：：：**表名*=*关联名称*[ 左&#124; 右 &#124; 完整]  
  
 外部联接=*表名*=*关联名称*[ &#124;*外部联接*= 打开  
  
 *搜索-*  
  
 *条件*  
  
 *关联名称*：：**用户定义名称*  
  
 *ODBC-esc -发物人*：：*  
  
 *ODBC-esc 终结器*：*|  
  
 要确定支持此语句的哪些部分，应用程序使用SQL_OJ_CAPABILITIES信息类型调用**SQLGetInfo。** 对于外部联接，*搜索条件*必须仅包含指定*表名*之间的联接条件。
