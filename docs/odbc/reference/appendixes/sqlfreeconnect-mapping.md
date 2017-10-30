---
title: "SQLFreeConnect 映射 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLFreeConnect
- SQLFreeConnect function [ODBC], mapping
ms.assetid: 8a844538-93c0-4709-bab6-35c45e771d80
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f83eaaf01bb828963f6ebe98b78f70461346b763
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfreeconnect-mapping"></a>SQLFreeConnect 映射
在应用程序调用**SQLFreeConnect**到 ODBC 3*.x*驱动程序，将会调用  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 映射到  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 与*处理*参数设置中的值为*hdbc*。

