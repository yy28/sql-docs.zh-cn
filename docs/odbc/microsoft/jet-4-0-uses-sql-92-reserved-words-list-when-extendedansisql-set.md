---
title: Jet 4.0 在 ExtendedAnsiSQL_Set 时使用 SQL-92 保留字列表 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], reserved words
ms.assetid: 7645187e-7777-4c07-9686-0a80d5c5834d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6988e0da1ecb881e0f6e88e35b66f1a6284f9b7a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299957"
---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisql_set"></a>在 ExtendedAnsiSQL_Set 的情况下，Jet 4.0 使用 SQL-92 保留字列表
启用 ExtendedAnsiSQL 标志后，Jet 4.0 将使用 SQL-92 保留字列表。 尝试使用 SQL-92 保留字作为未加引号的对象名称会导致语法错误。 关闭 ExtendedAnsiSQL 标志后，新的保留字可像以前一样用作对象名称。
