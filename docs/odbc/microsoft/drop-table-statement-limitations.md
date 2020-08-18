---
description: DROP TABLE 语句限制
title: DROP TABLE 语句限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, DROP TABLE statement limitations
- DROP TABLE statement limitations [ODBC]
ms.assetid: 0a1c80f5-c9f2-4655-9bfd-0131b2f015a9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9d56e53d8a17c15736e9423e5920c81f864e2973
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412553"
---
# <a name="drop-table-statement-limitations"></a>DROP TABLE 语句限制
当使用 Microsoft Excel 5.0、7.0 或97驱动程序时，DROP TABLE 语句将清除工作表，但不会删除工作表名称。 由于工作簿中仍存在工作表名称，因此不能用相同的名称创建其他工作表。
