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
ms.openlocfilehash: bc37ef6d268dba71f8270909ea9c5b938ef3ee75
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070492"
---
# <a name="procedure-invocation"></a>过程调用
使用 Microsoft Access 驱动程序时，可以使用**SQLExecDirect**或**SQLPrepare**函数通过以下语法从驱动程序调用过程： {CALL *procedure-name* [（*parameter*[，*parameter*] ...）]}。 请注意，表达式不支持作为被调用过程的参数。  
  
 如果过程名称包括破折号，则该名称必须用后面的引号（'）分隔。  
  
 可以使用前一语句调用参数化查询。
