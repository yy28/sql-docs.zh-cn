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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93d23216db950ed861449061f3e35e5e88a637fb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68058789"
---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisql_set"></a>在 ExtendedAnsiSQL_Set 的情况下，Jet 4.0 使用 SQL-92 保留字列表
启用 ExtendedAnsiSQL 标志后，Jet 4.0 将使用 SQL-92 保留字列表。 尝试使用 SQL-92 保留字作为未加引号的对象名称会导致语法错误。 关闭 ExtendedAnsiSQL 标志后，新的保留字可像以前一样用作对象名称。
