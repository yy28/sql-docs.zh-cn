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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107286"
---
# <a name="state-transition-checks"></a>状态转换检查
驱动程序管理器检查的环境、 连接或语句的状态适用于所调用的函数。 例如，连接必须是在一个已分配状态时**SQLConnect**称为; 语句必须是中的已准备运行时**SQLExecute**调用。 驱动程序管理器的状态转换错误将返回 SQL_ERROR。
