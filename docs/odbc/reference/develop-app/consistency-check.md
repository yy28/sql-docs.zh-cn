---
description: 一致性检查
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ad1ffe0cb7819447a3819d73cd6605347b756ede
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465899"
---
# <a name="consistency-check"></a>一致性检查
每当应用程序设置 APD、ARD 或 IPD 的 SQL_DESC_DATA_PTR 字段时，驱动程序就会自动执行一致性检查。 只要设置了此字段，驱动程序就会检查 SQL_DESC_TYPE 字段的值以及适用于同一记录中的 SQL_DESC_TYPE 字段的值是否有效且一致。  
  
 通常不会设置 IPD 的 SQL_DESC_DATA_PTR 字段;但是，应用程序可以执行此操作来强制执行 IPD 字段的一致性检查。 将 IPD 的 SQL_DESC_DATA_PTR 字段设置为的值实际上并不存储，无法通过对 **SQLGetDescField** 或 **SQLGetDescRec**的调用来检索。设置仅用于强制执行一致性检查。 不能对 IRD 执行一致性检查。  
  
 有关一致性检查的详细信息，请参阅 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。
