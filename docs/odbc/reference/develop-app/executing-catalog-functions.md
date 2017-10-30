---
title: "执行目录函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- catalog functions [ODBC], executing
- functions [ODBC], catalog functions
ms.assetid: c59cbda3-e214-4399-9edc-cfac86b378d7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 489cd057a15e90794c71cfb433931cd9bc687016
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="executing-catalog-functions"></a>执行目录函数
目录函数将创建一个结果集，因为它等效于执行任何结果集生成 SQL 语句。 事实上，执行预定义的 SQL 语句或调用附带的驱动程序或 DBMS 的预定义的过程通常实现目录函数。 几乎所有内容都适用于创建结果集的 SQL 语句也适用于目录函数。 例如，SQL_ATTR_MAX_ROWS 语句属性限制的目录函数，返回的行数，就像它限制返回的行数**选择**语句。  
  
 若要执行的目录函数，应用程序只需调用该函数。  
  
 有关目录函数的详细信息，请参阅[目录函数](../../../odbc/reference/develop-app/catalog-functions.md)。

