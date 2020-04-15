---
title: 转换规则 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], literals
- conversions with numeric literals [ODBC]
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: 89f846a3-001d-496a-9843-ac9c38dc1762
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c49177d62fffc3b3b5c47a25bf3fb421d7564245
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305083"
---
# <a name="rules-for-conversions"></a>转换规则
本节中的规则适用于涉及数字文本的转换。 就这些规则而言，定义了以下术语：  
  
-   *存储分配：* 将数据发送到数据库中的表列时。 这发生在对**SQLExecute、SQLExecDirect****和**的调用期间。 **SQLExecDirect** 在存储分配期间，"目标"是指数据库列，"源"是指应用程序缓冲区中的数据。  
  
-   *检索分配：* 将数据从数据库检索到应用程序缓冲区时。 这发生在对**SQLFetch、SQLGetData、SQLFetchScroll**和**SQLSetPos**的调用期间。 **SQLFetch** **SQLFetchScroll** 在检索分配期间，"目标"是指应用程序缓冲区，"源"是指数据库列。  
  
-   *CS：* 字符源中的值。  
  
-   *NT：* 数值目标中的值。  
  
-   *NS：* 数值源中的值。  
  
-   *CT：* 字符目标中的值。  
  
-   精确数字文本的精度：它包含的数字数。  
  
-   精确数字文本的刻度：明示或隐含期间右侧的数字数。  
  
-   近似数字文本的精度：其曼蒂萨的精度。  
  
## <a name="character-source-to-numeric-target"></a>字符源到数字目标  
 以下是从字符源 （CS） 转换为数字目标 （NT） 的规则：  
  
1.  将 CS 替换为通过删除 CS 中的任何前导空格或尾随空格而获得的值。 如果 CS 不是有效的*数字文本*，则返回 SQLSTATE 22018（强制转换规范的无效字符值）。  
  
2.  将 CS 替换为通过删除小数点前的前导零、在小数点之后尾随零或两者两者，获得的值。  
  
3.  将 CS 转换为 NT。 如果转换导致重要数字丢失，则返回 SQLSTATE 22003（数值范围外）。 如果转换导致非有效数字丢失，则返回 SQLSTATE 01S07（分数截断）。  
  
## <a name="numeric-source-to-character-target"></a>数字源到字符目标  
 以下是从数字源 （NS） 转换为字符目标 （CT） 的规则：  
  
1.  让 LT 以 CT 字符表示长度。 对于检索赋值，LT 等于字符中的缓冲区长度减去此字符集的 null 终止字符中的字节数。  
  
2.  例：  
  
    -   如果 NS 是精确数值类型，则让 YP 等于符合*精确数字文本*定义的最短字符串，以便 YP 的比例与 NS 的比例相同，而 YP 的解释值是 NS 的绝对值。  
  
    -   如果 NS 是近似数值类型，则让 YP 成为字符串，如下所示：  
  
         大小写：  
  
         如果 NS 等于 0，则 YP 为 0。  
  
         让 YSN 成为符合精确*数字文本*定义的最短字符串，其解释值是 NS 的绝对值。 如果 YSN 的长度小于 NS 数据类型的 （*精度*= 1），则让 YP 等于 YSN。  
  
         否则，YP 是符合*近似数字文本*定义的最短字符串，其解释值是 NS 的绝对值，其*符号*由不是"0"的单个*数字*组成，后跟句*点*和无*符号整数*。  
  
3.  大小写：  
  
    -   如果 NS 小于 0，则让 Y 成为以下结果：  
  
         '-' &#124;&#124; YP  
  
         其中"&#124;&#124;"是字符串串联运算符。  
  
         否则，让 Y 等于 YP。  
  
4.  让 LY 以 Y 字符的长度。  
  
5.  大小写：  
  
    -   如果 LY 等于 LT，则 CT 设置为 Y。  
  
    -   如果 LY 小于 LT，则 CT 按适当数量的空格在右侧设置为 Y 扩展。  
  
         否则（LY > LT），将 Y 的第一个 LT 字符复制到 CT 中。  
  
         大小写：  
  
         如果这是存储分配，则返回错误 SQLSTATE 22001（字符串数据，右截断）。  
  
         如果这是检索分配，则返回警告 SQLSTATE 01004（字符串数据，右截断）。 当复制导致小数位数丢失（尾随零以外的）时，驱动程序定义是否发生以下情况之一：  
  
         （1） 驱动程序将 Y 中的字符串截截到适当的比例（也可以为零），并将结果写入 CT。  
  
         （2） 驱动程序将 Y 中的字符串舍入到适当的比例（也可以为零），并将结果写入 CT。  
  
         （3） 驱动程序既不截流也不转，只需将 Y 的第一个 LT 字符复制到 CT 中。
