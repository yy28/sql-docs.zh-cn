---
title: Jet 4.0 使用 SQL-92 保留的字列表时 extendedansisql 设定 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058789"
---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisqlset"></a>在 ExtendedAnsiSQL_Set 的情况下，Jet 4.0 使用 SQL-92 保留字列表
当打开 ExtendedAnsiSQL 标志时，Jet 4.0 使用 SQL-92 保留的字列表。 尝试使用 SQL-92 保留字，因为不带引号的对象名称会导致语法错误。 ExtendedAnsiSQL 标志处于关闭状态，当新的保留的字可用作对象名称作为之前。
