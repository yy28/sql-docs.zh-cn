---
title: Interval 转义序列 |Microsoft 文档
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
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e3a475170fed349a5bf85eb4f23bb93fe4ae804
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="interval-escape-sequences"></a>Interval 转义序列
ODBC 使用间隔文字的转义序列。 此转义序列的语法如下所示：  
  
 {*间隔文本*}  
  
 BNF 语法的*间隔文本*，请参阅[间隔文本语法](../../../odbc/reference/appendixes/interval-literal-syntax.md)本附录后面一节。  
  
 如果数据源支持 interval 数据类型，则支持间隔文字的转义序列。 应用程序应调用**SQLGetTypeInfo**来确定是否支持这些数据类型。
