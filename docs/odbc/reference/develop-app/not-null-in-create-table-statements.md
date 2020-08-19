---
description: CREATE TABLE 语句中的 NOT NULL
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 92d066ebb4bd6b712acaa71e0e752b3f0f27a3df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429219"
---
# <a name="not-null-in-create-table-statements"></a>CREATE TABLE 语句中的 NOT NULL
某些数据库（尤其是桌面数据库）不支持**CREATE TABLE**语句中的**not NULL**列约束。 有关详细信息，请参阅 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 函数说明中的 SQL_NON_NULLABLE_COLUMNS 选项。
