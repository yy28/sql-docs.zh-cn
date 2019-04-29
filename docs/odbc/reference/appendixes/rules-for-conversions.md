---
title: 转换规则 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3ecee500204303dfcbcd8e179b9cb9cb0a94bae
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63032923"
---
# <a name="rules-for-conversions"></a>转换规则
在本部分中的规则适用于涉及数值的转换。 出于这些规则，定义了以下术语：  
  
-   *将存储分配：* 当数据发送到数据库中的表列。 发生这种情况在对调用期间**SQLExecute**， **SQLExecDirect**，并**SQLSetPos**。 在应用商店分配期间"目标"是指数据库列和"源"是指应用程序缓冲区中的数据。  
  
-   *检索分配：* 到应用程序缓冲区从数据库检索数据。 发生这种情况在对调用期间**SQLFetch**， **SQLGetData**， **SQLFetchScroll**，以及**SQLSetPos**。 在检索分配期间"目标"是指应用程序缓冲区和"源"是指数据库列。  
  
-   *CS:* 字符源中的值。  
  
-   *NT:* 数值的目标中的值。  
  
-   *NS:* 数值的源中的值。  
  
-   *CT:* 字符目标中的值。  
  
-   精确数值的精度： 它包含的数字个数。  
  
-   精确数值的小数位数： 明示或默示期右侧的位数。  
  
-   近似数值的精度： 其尾数的精度。  
  
## <a name="character-source-to-numeric-target"></a>字符源到数值的目标  
 下面是用于从字符源 (CS) 将转换为数值的目标 (NT) 的规则：  
  
1.  将获取通过在 CS 中删除任何前导或尾随空格的值替换为 CS。 如果不是有效 CS*数值文字*，返回 SQLSTATE 22018 （为转换指定无效的字符值）。  
  
2.  将获取通过删除之前小数点，尾随的小数点后面的零或两个前导零的值替换为 CS。  
  
3.  转换为 NT CS。 如果转换导致重要数字丢失，则返回 SQLSTATE 22003 （数值超出范围）。 如果转换导致 SQLSTATE 01S07 非重要数字丢失返回 （小数部分截断）。  
  
## <a name="numeric-source-to-character-target"></a>数值源到字符目标  
 下面是用于将其从数值源 (NS) 转换为字符目标 (CT) 的规则：  
  
1.  让 l T 是以字符为单位的 CT.长度 检索分配的 l T 等于缓冲区的长度中减去此字符集的 null 终止字符中的字节数的字符。  
  
2.  用例：  
  
    -   如果 NS 确切的数值类型，然后让等于符合定义的最短字符串 YP*精确数值文字*YP 的小数位数为相同的 NS 和小数位数并 YP 的解释型值NS 的绝对值。  
  
    -   如果 NS 近似数值类型，然后让 YP，如下所示为字符字符串：  
  
         用例：  
  
         如果 NS 等于 0，则 YP 为 0。  
  
         让 YSN 是符合的确切的定义的字符串最短*数值文字*和其已解释的值是 NS 的绝对值。 如果 YSN 的长度小于 (*精度*+ 1) 的 NS 的数据类型，然后让 YP 等于 YSN。  
  
         否则，YP 是符合的定义的字符最短的字符串*近似数值文字*其已解释的值是绝对值的数值的 NS 和其*尾数*组成单一*数字*，它是不"0"后, 跟*段*和一个*无符号整数*。  
  
3.  用例：  
  
    -   如果 NS 小于 0，然后让 Y 是导致的：  
  
         '-' &#124;&#124; YP  
  
         其中&#124;&#124;是字符串串联运算符。  
  
         否则，请允许 Y 等于 YP。  
  
4.  让 LY 为以字符为单位的 Y 的长度。  
  
5.  用例：  
  
    -   如果 LY 等于 l T，然后 CT 设置为 Y。  
  
    -   如果 LY 小于 l T，然后 CT 设置为 Y 扩展在右侧的适当数量的空格。  
  
         否则为 (LY > l T)，将 Y 的第一个 l T 字符复制到 CT.  
  
         用例：  
  
         如果这是一个应用商店分配，则返回错误 SQLSTATE 22001 （字符串数据，右端被截断）。  
  
         如果这是检索赋值，则返回警告 SQLSTATE 01004 （字符串数据，右端被截断）。 副本都会导致的 （而不是尾随零） 的小数位数的丢失，时，驱动程序定义是否发生以下情况之一：  
  
         （1） 该驱动程序将截断到适当规模 （它也可以是零） 中 Y 的字符串，并将结果写入到 CT.  
  
         （2） 该驱动程序将舍入到适当规模 （它也可以是零） 中 Y 的字符串，并将结果写入到 CT.  
  
         （3) 驱动程序都不会截断，也不将舍入，但只是将 Y 的第一个 l T 字符复制到 CT.
