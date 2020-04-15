---
title: 一致性检查 |微软文档
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
ms.openlocfilehash: edd946ca865cd9d8d2edff2c7bedbb3b2629c97c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298997"
---
# <a name="consistency-check"></a>一致性检查
每当应用程序设置 APD、ARD 或 IPD 的SQL_DESC_DATA_PTR字段时，驱动程序会自动执行一致性检查。 每当设置此字段时，驱动程序都会检查SQL_DESC_TYPE字段的值和适用于同一记录中SQL_DESC_TYPE字段的值是否有效且一致。  
  
 通常不设置 IPD 的SQL_DESC_DATA_PTR字段;但是，应用程序可以这样做来强制对 IPD 字段进行一致性检查。 IPD 的SQL_DESC_DATA_PTR字段的值实际上未存储，并且无法通过调用**SQLGetDescField**或**SQLGetDescRec**检索该值。设置仅用于强制一致性检查。 无法对 IRD 执行一致性检查。  
  
 有关一致性检查的详细信息，请参阅[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。
