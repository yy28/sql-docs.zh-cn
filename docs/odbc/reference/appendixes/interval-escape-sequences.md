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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041642"
---
# <a name="interval-escape-sequences"></a>间隔转义序列
ODBC 对间隔文本使用转义序列。 此转义序列的语法如下所示：  
  
 {*间隔文本*}  
  
 有关*间隔文本*的 BNF 语法，请参阅本附录后面的 "[时间段文本语法](../../../odbc/reference/appendixes/interval-literal-syntax.md)" 部分。  
  
 如果数据源支持间隔数据类型，则支持间隔文本转义序列。 应用程序应调用**SQLGetTypeInfo** ，以确定是否支持这些数据类型。
