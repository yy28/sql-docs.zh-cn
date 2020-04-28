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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d19cde2d531819a60229dd7a780181571e169503
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307778"
---
# <a name="supported-data-types"></a>支持的数据类型
Dbms 支持的数据类型差别很大。 应用程序可以通过调用**SQLGetTypeInfo**来确定支持的数据类型的名称和特性。 由于数据类型名称的变化很大，因此应用程序必须使用**SQLGetTypeInfo**在**CREATE TABLE**语句中返回的数据类型名称。 有关详细信息，请参阅[ODBC 中的数据类型](../../../odbc/reference/develop-app/data-types-in-odbc.md)。
