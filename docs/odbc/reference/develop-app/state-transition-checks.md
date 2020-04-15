---
title: 状态转换检查 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7dc1ddc126a2d652dfdb038cbb0e510f9735d7b0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299702"
---
# <a name="state-transition-checks"></a>状态转换检查
驱动程序管理器检查环境、连接或语句的状态是否适合被调用的函数。 例如，在调用**SQLConnect**时，连接必须处于分配状态;调用**SQLExecute**时，语句必须处于准备状态。 驱动程序管理器返回SQL_ERROR状态转换错误。
