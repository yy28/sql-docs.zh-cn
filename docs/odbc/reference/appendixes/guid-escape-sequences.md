---
title: GUID 转义序列 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], GUID
- escape sequences [ODBC], guid
- guid escape sequence [ODBC]
ms.assetid: 71d43ef9-4a31-493e-b9e0-f864e9ef3ce6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5edd631171acf78fd4c0ada857f72e4e50fd5ebe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="guid-escape-sequences"></a>GUID 转义序列
ODBC 使用 GUID 文字的转义序列。 此转义序列的语法如下所示：  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>注释  
 BNF 表示法中的语法，如下所示是：  
  
 *ODBC guid 转义*:: =  
     *ODBC esc 启动器 guid* *guid 值* *ODBC esc 终止符*  
  
 *ODBC esc 启动器*:: = {  
  
 *ODBC esc 终止符*:: =}  
  
 *guid 值*:: =*时钟低值 guid 分隔符时钟中间值 guid 分隔符时钟高价值 guid 分隔符时钟 seq 值 guid 分隔符节点值*  
  
 *guid 分隔符*:: =-  
  
 *时钟低价值*:: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *时钟中间值*:: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *时钟高价值*:: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *时钟 seq 值*:: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *时钟节点值*:: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *hex_digit* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; A &#124; B &#124; C &#124; D &#124; E &#124; F  
  
 如果 GUID 数据类型支持的数据源，支持 GUID 文字的转义序列。 应用程序应调用**SQLGetTypeInfo**来确定是否支持此数据类型。
