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
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLFreeEnv function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLFreeEnv
ms.assetid: c0f76455-d072-4bae-bee7-452277dfa479
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c2aa64e5ca6e64932c4362603dc370ab02f7c962
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
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
