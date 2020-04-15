---
title: 执行目录函数 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6469a5394e232ab9d9135fbbbd56ba7b791ccbcb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305718"
---
# <a name="executing-catalog-functions"></a>执行目录函数
由于目录函数创建结果集，因此等效于执行任何结果集生成的 SQL 语句。 事实上，目录函数通常是通过执行预定义的 SQL 语句或调用驱动程序或 DBMS 附带的预定义过程实现的。 几乎所有适用于创建结果集的 SQL 语句都适用于目录函数。 例如，SQL_ATTR_MAX_ROWS语句属性限制目录函数返回的行数，就像它限制**SELECT**语句返回的行数一样。  
  
 要执行目录函数，应用程序只需调用该函数。  
  
 有关目录函数的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。
