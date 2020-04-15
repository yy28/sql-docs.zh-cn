---
title: GUID 转义序列 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], GUID
- escape sequences [ODBC], guid
- guid escape sequence [ODBC]
ms.assetid: 71d43ef9-4a31-493e-b9e0-f864e9ef3ce6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44907bfbd884bf361ce5f2ab8b3f6d8a247aba44
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306968"
---
# <a name="guid-escape-sequences"></a>GUID 转义序列
ODBC 使用转义序列进行 GUID 文本。 此转义序列的语法如下：  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>备注  
 在 BNF 符号中，语法如下所示：  
  
 *ODBC-guid 转义*：：*  
     *ODBC-esc-开始器 guid*'*吉德值*' *ODBC-esc 终结器*  
  
 *ODBC-esc -发物人*：：*  
  
 *ODBC-esc 终结器*：*|  
  
 *guid 值*：：： =*时钟-低值 guid-分隔符时钟-中间值 guid-分隔符-高值 guid-分离器时钟-值 guid-分离器节点值*  
  
 *吉德分离器*：：* -  
  
 *时钟低值*：：* *hex_digit hex_digithex_digit hex_digithex_digithex_digit hex_digithex_digithex_digithex_digithex_digit*  
  
 *时钟中间值*：：* *hex_digithex_digithex_digithex_digit*  
  
 *时钟高值*：：* *hex_digithex_digithex_digithex_digit*  
  
 *时钟-seq 值*：：* *hex_digithex_digithex_digithex_digit*  
  
 *时钟节点值*：：* *hex_digithex_digithex_digit hex_digit hex_digithex_digit hex_digit hex_digithex_digithex_digithex_digithex_digithex_digithex_digithex_digit*  
  
 *hex_digit* ：：* 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; a &#124; B &#124; C &#124; &#124; E &#124; F  
  
 如果数据源支持 GUID 数据类型，则支持 GUID 文本转义序列。 应用程序应调用**SQLGetTypeInfo**以确定是否支持此数据类型。
