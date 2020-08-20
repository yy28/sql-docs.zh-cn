---
description: 状态转换检查
title: 状态转换检查 |Microsoft Docs
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
ms.openlocfilehash: 50a845f2b83ada7c9d4f03f252b6d2bc3d3eff3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476369"
---
# <a name="state-transition-checks"></a>状态转换检查
驱动程序管理器检查环境、连接或语句的状态是否适用于正在调用的函数。 例如，当调用 **SQLConnect** 时，连接必须处于已分配状态;调用 **SQLExecute** 时，语句必须处于已准备状态。 对于状态转换错误，驱动程序管理器返回 SQL_ERROR。
