---
title: 一致性检查 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], consistency checks
- consistency checks [ODBC]
ms.assetid: deb80efa-ad1f-4ea5-b334-9817cd279e5c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c2711f7d45ba433d97c36adb83b8400c6a386eac
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="consistency-check"></a>一致性检查
一致性检查时，将执行由驱动程序会自动应用程序设置 APD、 ARD 或 IPD SQL_DESC_DATA_PTR 字段。 每当设置此字段时，驱动程序将检查 SQL_DESC_TYPE 字段的值和适用于同一记录中的 SQL_DESC_TYPE 字段值有效且一致。  
  
 通常情况下不设置 IPD SQL_DESC_DATA_PTR 字段;但是，应用程序可以这样做是为了强制 IPD 字段执行一致性检查。 IPD SQL_DESC_DATA_PTR 字段设置为的值不会实际存储，不能通过调用检索**SQLGetDescField**或**SQLGetDescRec**; 进行设置仅用于强制一致性检查。 不能在 IRD 上执行一致性检查。  
  
 有关一致性检查的详细信息，请参阅[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。
