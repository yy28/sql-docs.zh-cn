---
title: 间隔转义序列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 69c674ee8838273af9bf4ed91ddcead7e1768fb9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041642"
---
# <a name="interval-escape-sequences"></a>间隔转义序列
ODBC 使用间隔文字的转义序列。 此转义序列的语法如下所示：  
  
 {*interval-literal*}  
  
 有关的 BNF 语法*间隔文字*，请参阅[间隔文本语法](../../../odbc/reference/appendixes/interval-literal-syntax.md)本附录中稍后的部分。  
  
 如果数据源支持 interval 数据类型，支持间隔文字的转义序列。 应用程序应调用**SQLGetTypeInfo**来确定是否支持这些数据类型。
