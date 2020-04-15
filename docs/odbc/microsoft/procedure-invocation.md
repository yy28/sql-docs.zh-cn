---
title: 过程调用 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32617cdb753f5fc1b9c52520cb609d2902137b54
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290768"
---
# <a name="procedure-invocation"></a>过程调用
使用 Microsoft Access 驱动程序时，可以使用**SQLExecDirect**或**SQLPrepare**函数使用具有以下语法，从驱动程序调用过程：[CALL*过程名称*]（*参数*[，*参数*]...）]。 请注意，表达式不支持作为调用过程的参数。  
  
 如果过程名称包含破折号，则必须使用回引号 （'） 分隔名称。  
  
 可以使用前面的语句调用参数化查询。
