---
title: 在 CREATE TABLE 语句中为 NOT NULL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 808cddbd805db09d1b5c356d5b5af5734a5dcc16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086318"
---
# <a name="not-null-in-create-table-statements"></a>CREATE TABLE 语句中的 NOT NULL
某些数据库（尤其是桌面数据库）不支持**CREATE TABLE**语句中的**not NULL**列约束。 有关详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明中的 SQL_NON_NULLABLE_COLUMNS 选项。
