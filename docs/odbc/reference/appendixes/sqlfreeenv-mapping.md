---
title: "SQLFreeEnv 映射 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLFreeEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeEnv
ms.assetid: c0f76455-d072-4bae-bee7-452277dfa479
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a5c1dae2fb67d530e9e8bfefd041eb978eb5bf15
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfreeenv-mapping"></a>SQLFreeEnv 映射
在应用程序调用**SQLFreeEnv**到 ODBC 3*.x*驱动程序，将会调用  
  
```  
SQLFreeEnv(henv)   
```  
  
 映射到  
  
```  
SQLFreeHandle(SQL_HANDLE_ENV,Handle)  
```  
  
 与*处理*参数设置中的值为*henv*。

