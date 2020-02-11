---
title: 执行目录函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], executing
- functions [ODBC], catalog functions
ms.assetid: c59cbda3-e214-4399-9edc-cfac86b378d7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab6eba9c4a3df3e16e35d8a93dc95209a093fb80
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67901278"
---
# <a name="executing-catalog-functions"></a>执行目录函数
由于目录函数会创建一个结果集，因此它等效于执行任何结果集生成的 SQL 语句。 事实上，通常通过执行预定义的 SQL 语句或调用驱动程序或 DBMS 附带的预定义过程来实现目录函数。 几乎所有适用于创建结果集的 SQL 语句的内容也适用于目录函数。 例如，SQL_ATTR_MAX_ROWS 语句特性会限制目录函数返回的行数，就像它限制**SELECT**语句返回的行数。  
  
 若要执行目录函数，应用程序只需调用函数。  
  
 有关目录函数的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。
