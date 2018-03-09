---
title: "按序号加载 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backward compatibility [ODBC], loading by ordinal
- compatibility [ODBC], loading by ordinal
- loading by ordinal [ODBC]
ms.assetid: 337d90ab-68eb-4940-a2f3-f7d5693ee766
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 831ee6a9e990942fa5fbaa336d5dd9e296429826
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="loading-by-ordinal"></a>按序号加载
在 ODBC 2。*x*，无法执行加载序号以提高在连接过程中的性能。 一个 ODBC 2。*x*驱动程序导出具有序号 199 的虚函数; 当驱动程序管理器检测到它，它按序号而不是按名称解析 ODBC 函数的地址。 ODBC 2 仍支持此功能。*x*驱动程序，但不是支持 ODBC 3*.x*驱动程序。
