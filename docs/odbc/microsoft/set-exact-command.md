---
title: 设置精确命令 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e754fff35b6b948ac63d19361067b2d65a07fdd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300867"
---
# <a name="set-exact-command"></a>SET EXACT 命令
指定用于比较两个不同长度的字符串的规则。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 指定表达式必须匹配字符，字符为等效字符。 对于比较，将忽略表达式中的任何尾随空格。 为了进行比较，两个表达式的较短时间在右侧用空格填充，以匹配较长表达式的长度。  
  
 OFF  
 （默认值。指定要等效的是，表达式必须匹配字符的字符，直到到达右侧表达式的末尾。  
  
## <a name="remarks"></a>备注  
 如果两个字符串的长度相同，则 SET EXACT 设置不起作用。  
  
## <a name="string-comparisons"></a>字符串比较  
 Visual FoxPro 有两个关系运算符，用于测试相等性。  
  
 _ 运算符对相同类型的两个值执行比较。 此运算符适用于比较字符、数字、日期和逻辑数据。  
  
 但是，当您将字符表达式与 + 运算符进行比较时，结果可能不完全是您期望的结果。 字符表达式从左到右比较字符的字符，直到其中一个表达式不等于另一个表达式，直到到达 _ 运算符右侧的表达式的末尾（SET EXACT OFF），或直到达到两个表达式的末尾（SET EXACT ON）。  
  
 当需要精确比较字符数据时，可以使用 * 运算符。 如果将两个字符表达式与 * 运算符进行比较，则 _ 运算符两侧的表达式必须包含完全相同的字符（包括空白）才能被视为相等。 使用 *比较字符串时，将忽略 SET EXACT 设置。  
  
 下表显示了运算符的选择和 SET EXACT 设置如何影响比较。 （下划线表示空白。  
  
|比较|• 完全关闭|• 精确打开|• 精确打开或关闭|  
|----------------|------------------|-----------------|--------------------------|  
|"abc" = "abc"|匹配|匹配|匹配|  
|"ab" = "abc"|无匹配|无匹配|无匹配|  
|"abc" = "ab"|匹配|无匹配|无匹配|  
|"abc" = "ab_"|无匹配|无匹配|无匹配|  
|"ab" = "ab_"|无匹配|匹配|无匹配|  
|"ab_" = "ab"|匹配|匹配|无匹配|  
|"" = "ab"|无匹配|无匹配|无匹配|  
|"ab" = ""|匹配|无匹配|无匹配|  
|"__" = ""|匹配|匹配|无匹配|  
|"" = "___"|无匹配|匹配|无匹配|  
|修剪（"*"） = ""|匹配|匹配|匹配|  
|"" = 修剪（"*"|匹配|匹配|匹配|  
  
## <a name="see-also"></a>另请参阅  
 [SET ANSI 命令](../../odbc/microsoft/set-ansi-command.md)
