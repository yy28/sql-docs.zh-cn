---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b337d317092ad6ae20cc91236d69c1314de96bce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107286"
---
# <a name="state-transition-checks"></a>状态转换检查
驱动程序管理器检查环境、连接或语句的状态是否适用于正在调用的函数。 例如，当调用**SQLConnect**时，连接必须处于已分配状态;调用**SQLExecute**时，语句必须处于已准备状态。 对于状态转换错误，驱动程序管理器返回 SQL_ERROR。
