---
description: 间隔转义序列
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e2ef792403352568ce5f8d92c07a5b0e1027b507
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483290"
---
# <a name="interval-escape-sequences"></a>间隔转义序列
ODBC 对间隔文本使用转义序列。 此转义序列的语法如下所示：  
  
 {*间隔文本*}  
  
 有关 *间隔文本*的 BNF 语法，请参阅本附录后面的 " [时间段文本语法](../../../odbc/reference/appendixes/interval-literal-syntax.md) " 部分。  
  
 如果数据源支持间隔数据类型，则支持间隔文本转义序列。 应用程序应调用 **SQLGetTypeInfo** ，以确定是否支持这些数据类型。
