---
title: 多个 hstmt （Paradox 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5e7a9a4ec0d6426779fb55d923bc7f0607089aad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045029"
---
# <a name="multiple-hstmts-paradox-driver"></a>多个 hstmt（Paradox 驱动程序）
使用 ODBC Paradox 驱动程序时，如果想要使用多个*hstmt*若要对表执行查询，表必须具有唯一索引 （Paradox 主键）。
