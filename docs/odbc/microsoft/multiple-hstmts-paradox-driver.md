---
description: 多个 hstmt（Paradox 驱动程序）
title: 多个 hstmt (Paradox 驱动程序) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- multiple hstmts [ODBC]
- Paradox driver [ODBC], multiple hstmts
ms.assetid: 66aecd94-092d-43d4-9583-74f5e2990eac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 687b87f07142ad23f6faf7155ae974a6d93deab4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449399"
---
# <a name="multiple-hstmts-paradox-driver"></a>多个 hstmt（Paradox 驱动程序）
当使用 ODBC Paradox 驱动程序时，如果要使用多个 *hstmt* 来对表执行查询，则表必须具有唯一索引 (Paradox 主键) 。
