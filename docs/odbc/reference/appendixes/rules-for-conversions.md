---
title: "转换规则 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- numeric data type [ODBC], literals
- conversions with numeric literals [ODBC]
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: 89f846a3-001d-496a-9843-ac9c38dc1762
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 06baaaff03f75cbf04da86527a25ea60755a473e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="rules-for-conversions"></a>转换规则
本部分中的规则适用于涉及数值的转换。 对于这些规则，定义了以下术语：  
  
-   *存储分配：*时将数据发送到数据库中的表列。 发生这种情况在调用过程**SQLExecute**， **SQLExecDirect**，和**SQLSetPos**。 在应用商店分配过程中，"目标"引用的数据库列和"源"是指应用程序缓冲区中的数据。  
  
-   *检索分配：*到应用程序缓冲区从数据库检索数据时。 发生这种情况在调用过程**SQLFetch**， **SQLGetData**， **SQLFetchScroll**，和**SQLSetPos**。 在检索分配过程中，"目标"是指应用程序缓冲区和"源"引用的数据库列。  
  
-   *CS:*字符源中的值。  
  
-   *NT:*数值的目标中的值。  
  
-   *NS:*数值源中的值。  
  
-   *CT:*字符目标中的值。  
  
-   精确数值精度： 它包含的数字个数。  
  
-   精确数值的小数位数： 明示或暗示段右侧的数字个数。  
  
-   近似数值的精度： 其尾数的精度。  
  
## <a name="character-source-to-numeric-target"></a>字符源到数值的目标  
 下面是用于将其从字符源 (CS) 转换为数值的目标 (NT) 的规则：  
  
1.  CS 替换获取通过在 CS 中删除任何前导空格或尾随空格的值。 如果不是有效 CS*数字文本*，返回 SQLSTATE 22018 （为转换指定的无效字符值）。  
  
2.  CS 替换获取通过删除尾随的小数点后面的零或两个小数点前的前导零的值。  
  
3.  将 CS 转换为 NT。 如果转换导致重要数字丢失，则返回 SQLSTATE 22003 （超出范围的数字值）。 如果转换导致的无意义的数字，SQLSTATE 01S07 丢失返回 （小数截断）。  
  
## <a name="numeric-source-to-character-target"></a>指向字符的数值源  
 下面是用于将其从数值源 (NS) 转换为字符目标 (CT) 的规则：  
  
1.  让 LT 为以字符为单位的 CT.长度 检索分配的 LT 等于缓冲区的长度以字符减去此字符集的 null 终止字符中的字节数为单位。  
  
2.  情况：  
  
    -   如果 NS 是精确数值类型，然后让 YP 等于符合定义的最短的字符字符串*精确数值文本*YP 的小数位数为相同的 NS，小数位数并 YP 的解释型的值是NS 绝对值。  
  
    -   如果 NS 是近似数值类型，然后让 YP，如下所示为字符字符串：  
  
         情况：  
  
         如果 NS 等于 0，则 YP 为 0。  
  
         让 YSN 是最短的字符字符串的确切-定义符合*数字文本*并且其解释的值的 NS 绝对值的数值。 如果 YSN 的长度小于 (*精度*+ 1) 的 NS 的数据类型，然后让 YP 等于 YSN。  
  
         否则，YP 是符合的定义的最短字符字符串*近似数值文本*其解释的值是绝对值的数值的 NS 和其*尾数*组成单个*数字*，它是不 '0' 后, 跟*段*和*无符号整数*。  
  
3.  情况：  
  
    -   如果 NS 小于 0，然后让 Y 是导致的：  
  
         -&#124; &#124;YP  
  
         其中 &#124; &#124; 是字符串串联运算符。  
  
         否则，让 Y 等于 YP。  
  
4.  让 LY 为以字符为单位的 Y 长度。  
  
5.  情况：  
  
    -   如果 LY 等于 LT，则 CT 设置为 Y。  
  
    -   如果 LY 小于 LT，则 CT 设置为 Y 扩展在右侧的适当数量的空格。  
  
         否则为 (LY > LT)，将 Y 的第一个 LT 字符复制到 CT.  
  
         情况：  
  
         如果这是存储分配，返回错误 SQLSTATE 22001 （字符串数据，右截断）。  
  
         如果这是检索赋值，则返回警告 SQLSTATE 01004 （字符串数据，右截断）。 副本都会导致的 （而不是尾随零） 的小数位数的丢失，时，驱动程序定义是否发生以下情况之一：  
  
         （1） 驱动程序将截断 y 连接到适当的比例 （它也可以是零） 的字符串，并将结果写入到 CT.  
  
         （2） 该驱动程序将舍入到适当的比例 （它也可以是零） 中 Y 的字符串，并将结果写入到 CT.  
  
         （3） 该驱动程序既不截断，也将舍入，但只需将 Y 的第一个 LT 字符复制到 CT.

