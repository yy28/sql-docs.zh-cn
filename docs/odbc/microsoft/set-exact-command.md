---
title: SET EXACT 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16651df836ac3fb87c5e28b4b8fa25088e9dd86a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63159340"
---
# <a name="set-exact-command"></a>SET EXACT 命令
指定用于比较不同长度的两个字符串的规则。  
  
## <a name="syntax"></a>语法  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>参数  
 ON  
 指定表达式必须匹配的字符才能等效。 比较会忽略在表达式中的任何尾随空格。 有关比较，较短的两个表达式填充右侧使用空白以符合较长表达式的长度。  
  
 OFF  
 （默认值）。指定，才能等效，表达式必须匹配的字符直至达到右侧表达式的末尾。  
  
## <a name="remarks"></a>备注  
 如果两个字符串的长度相同，则设置完全设置无效。  
  
## <a name="string-comparisons"></a>字符串比较  
 Visual FoxPro 具有测试相等的两个关系运算符。  
  
 = 运算符执行相同类型的两个值之间的比较。 此运算符适合比较字符、 数字、 日期和逻辑数据。  
  
 但是，进行比较时使用的字符表达式 = 运算符，则结果可能不是完全你期望的内容。 字符表达式进行比较字符的从左到右，直到其中一个表达式不等于另一个，直到在右侧表达式的末尾的字符 = 运算符达到 （设置完全关闭），或直到两个表达式结尾达到 (设置确切 ON)。  
  
 = = 需要的字符数据的精确比较时，可以使用运算符。 如果两个字符表达式比较使用 = = 运算符的两侧的表达式 = = 运算符必须包含完全相同的字符包括空格，将被视为相等。 使用比较字符串时，将忽略设置完全设置 = =。  
  
 下表显示了所选的运算符和完全设置的设置如何影响比较。 （下划线表示空格。）  
  
|比较|= 完全关闭|= 在确切|= = 确切 ON 或 OFF|  
|----------------|------------------|-----------------|--------------------------|  
|"abc" = "abc"|匹配项|匹配项|匹配项|  
|"ab" = "abc"|没有匹配项|没有匹配项|没有匹配项|  
|"abc" = "ab"|匹配项|没有匹配项|没有匹配项|  
|"abc" = "ab_"|没有匹配项|没有匹配项|没有匹配项|  
|"ab" = "ab_"|没有匹配项|匹配项|没有匹配项|  
|"ab_" = "ab"|匹配项|匹配项|没有匹配项|  
|""="ab"|没有匹配项|没有匹配项|没有匹配项|  
|"ab" = ""|匹配项|没有匹配项|没有匹配项|  
|"__" = ""|匹配项|匹配项|没有匹配项|  
|"" = "___"|没有匹配项|匹配项|没有匹配项|  
|TRIM("___") = ""|匹配项|匹配项|匹配项|  
|"" = TRIM("___")|匹配项|匹配项|匹配项|  
  
## <a name="see-also"></a>请参阅  
 [SET ANSI 命令](../../odbc/microsoft/set-ansi-command.md)
