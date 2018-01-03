---
title: "过程调用 |Microsoft 文档"
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
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 10af4e60b9fb30e8030d31f80c93681e73375e1e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="procedure-invocation"></a>过程调用
过程使用 Microsoft Access 驱动程序时，可以通过使用从驱动程序进行调用**SQLExecDirect**或**SQLPrepare**函数具有以下语法: {调用*过程名称* [(*参数*[，*参数*]...)]}。 请注意，作为参数调用的过程不支持表达式。  
  
 如果过程名称包括短划线，必须用后引号 （'） 分隔名称。  
  
 可以使用上一条语句调用参数化的查询。
