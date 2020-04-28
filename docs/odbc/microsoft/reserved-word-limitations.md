---
title: 保留字限制 |Microsoft Docs
ms.custom: ''
ms.date: 05/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ed42f083-c9e8-4ee4-9d64-d879bf955c78
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf536e06556e6b2e7b27f220d09a51f91b44d23c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304005"
---
# <a name="reserved-keyword-limitations"></a>保留关键字限制

避免在 SQL 表或相关对象中使用任何 ODBC 保留关键字作为标识符。 如果需要将保留关键字用作标识符，则必须使用*反撇号*（'）将标识符括起来。 *反撇号*的另一个名称是*后退引号*。

保留关键字限制还适用于保留关键字的任何简写形式。

ODBC 保留关键字的列表位于：

- [ODBC 保留关键字](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords)。

- 有关*ODBC 程序员参考指南*，请参阅[附录 C： SQL 语法](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar)。

