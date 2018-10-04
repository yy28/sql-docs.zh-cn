---
title: GUID 转义序列 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf41671abc6393a18fad06e1debd297fed1f04c5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654963"
---
# <a name="guid-escape-sequences"></a>GUID 转义序列
ODBC 使用 GUID 文字的转义序列。 此转义序列的语法如下所示：  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>备注  
 BNF 表示法中的语法是按如下所示：  
  
 *Guid 的 ODBC 转义*:: =  
     *ODBC esc 启动器 guid* '*guid 值* *ODBC esc 终止符*  
  
 *ODBC esc 启动器*:: = {  
  
 *ODBC esc 终止符*:: =}  
  
 *guid 值*:: =*时钟低价值 guid 分隔符时钟中间值 guid 分隔符时钟高价值 guid 分隔符时钟 seq 值 guid 分隔符节点值*  
  
 *guid 分隔符*:: =-  
  
 *时钟低价值*:: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *时钟中间值*:: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *时钟高价值*:: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *时钟 seq 值*:: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *节点值的时钟*:: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *hex_digit* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9&#124;的&#124;B &#124; C &#124; D &#124; E &#124; F  
  
 如果 GUID 数据类型支持的数据源，支持 GUID 文字的转义序列。 应用程序应调用**SQLGetTypeInfo**来确定是否支持此数据类型。
