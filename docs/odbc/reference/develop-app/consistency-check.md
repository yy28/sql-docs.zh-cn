---
title: 一致性检查 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], consistency checks
- consistency checks [ODBC]
ms.assetid: deb80efa-ad1f-4ea5-b334-9817cd279e5c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cb73d8a4de482f24eae5794232019af9890e3624
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727785"
---
# <a name="consistency-check"></a>一致性检查
一致性检查时，将执行由驱动程序会自动应用程序设置 SQL_DESC_DATA_PTR APD、 ARD 或 IPD 的字段。 只要设置此字段，该驱动程序将检查 SQL_DESC_TYPE 字段的值和适用于同一记录中的 SQL_DESC_TYPE 字段的值有效以及一致。  
  
 通常情况下未设置 SQL_DESC_DATA_PTR 字段 IPD 的;但是，应用程序可以这样做是为了强制执行一致性检查的 IPD 字段。 IPD 的 SQL_DESC_DATA_PTR 字段设置为的值实际上并不存储，无法通过调用检索**SQLGetDescField**或**SQLGetDescRec**; 进行设置仅用于强制一致性检查。 不能在 IRD 上执行一致性检查。  
  
 有关一致性检查的详细信息，请参阅[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。
