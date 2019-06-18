---
title: 过程调用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], procedure invocation
- procedure invocation [ODBC]
ms.assetid: b9ff2c3a-2003-4832-adbe-08dd0f5ad948
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7b33bc399646a6d274c875abd36d53219a2814e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200516"
---
# <a name="procedure-invocation"></a>过程调用
过程使用 Microsoft Access 驱动程序时，可以通过使用从驱动程序来调用**SQLExecDirect**或**SQLPrepare**函数具有以下语法: {调用*过程名称* [(*参数*[，*参数*]...)]}。 请注意，表达式不支持为被调用过程的参数。  
  
 如果过程名称中包含短划线，必须用单引号 （'）） 后分隔名称。  
  
 可以使用前面的语句调用参数化的查询。
