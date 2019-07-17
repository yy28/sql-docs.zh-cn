---
title: 支持的数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], DBMS support
- interoperability [ODBC], data types
ms.assetid: a89d4bab-ef3c-45c2-aa72-2639b3e0f856
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f5ec0f3943fd52540f094a23e9b3f9f3886e1371
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114081"
---
# <a name="supported-data-types"></a>支持的数据类型
支持的 Dbms 的数据类型差异相当大。 应用程序可以通过调用确定的名称和受支持的数据类型的特征**SQLGetTypeInfo**。 由于宽变体中数据的类型名称，该应用程序必须使用返回的数据类型名称**SQLGetTypeInfo**中**CREATE TABLE**语句。 有关详细信息，请参阅[ODBC 中的数据类型](../../../odbc/reference/develop-app/data-types-in-odbc.md)。
