---
title: Scalar 函数转义序列 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8347b8e6f0fab6dffc5295fb3b8260a6a56ed123
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305070"
---
# <a name="scalar-function-escape-sequence"></a>标量函数转义序列
ODBC 使用转义序列进行标量函数。 此转义序列的语法如下：  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>备注  
 在 BNF 符号中，语法如下所示：  
  
 *ODBC-标点-功能转义*：：*  
  
 *ODBC-esc-开始器*fn*标量函数 ODBC-esc 终结器*  
  
 *标量函数*：：**函数名称*（*参数列表*）  
  
 （非终端*函数名称*和*函数名称*（*参数列表*）的定义派生自附录 E 中的标量函数列表[：Scalar 函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。  
  
 *ODBC-esc -发物人*：：*  
  
 *ODBC-esc 终结器*：*|  
  
 要确定数据源是否支持过程，驱动程序支持 ODBC 过程调用语法，应用程序可以调用**SQLGetInfo**。 有关详细信息，请参阅附录[E：Scalar 函数](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。
