---
title: CREATE TABLE 语句中不为 NULL |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 4147e560d953b97ecba2e707d354bb6bf2ead59b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47834821"
---
# <a name="not-null-in-create-table-statements"></a>CREATE TABLE 语句中的 NOT NULL
某些数据库和尤其是桌面数据库不支持**NOT NULL**中的列约束**CREATE TABLE**语句。 有关详细信息，请参阅中的 SQL_NON_NULLABLE_COLUMNS 选项[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。
