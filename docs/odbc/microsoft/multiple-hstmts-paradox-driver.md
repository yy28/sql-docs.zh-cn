---
title: 多个 hstmt（悖论驱动程序） |微软文档
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
ms.openlocfilehash: ac381024a6b4b67719cb7c098367f63a6176bad0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298187"
---
# <a name="multiple-hstmts-paradox-driver"></a>多个 hstmt（Paradox 驱动程序）
使用 ODBC 悖论驱动程序时，如果要使用多个*hstmt*在表上执行查询，则表必须具有唯一索引（Paradox 主键）。
