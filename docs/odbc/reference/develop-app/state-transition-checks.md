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
manager: craigg
ms.openlocfilehash: dcfefffb167b97ace09bfa358296d886265a987f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809625"
---
# <a name="state-transition-checks"></a>状态转换检查
驱动程序管理器检查的环境、 连接或语句的状态适用于所调用的函数。 例如，连接必须是在一个已分配状态时**SQLConnect**称为; 语句必须是中的已准备运行时**SQLExecute**调用。 驱动程序管理器的状态转换错误将返回 SQL_ERROR。
