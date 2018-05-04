---
title: 状态转换检查 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58a02120f43de726a581fa43df2dba7593f302ae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="state-transition-checks"></a>状态转换检查
驱动程序管理器检查环境、 连接或语句的状态适用于被调用函数。 例如，连接必须为一个已分配状态时**SQLConnect**称为; 语句必须是中的已准备状态时**SQLExecute**调用。 驱动程序管理器返回 SQL_ERROR 状态转换错误。
