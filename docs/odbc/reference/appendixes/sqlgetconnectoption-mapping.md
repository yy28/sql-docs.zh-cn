---
title: SQLGetConnectOption 映射 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLGetConnectOption
- SQLGetConnectOption function [ODBC], mapping
ms.assetid: e3792fe4-a955-473a-a297-c1b2403660c4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ec36a536732299337efde3cf58cc98fbf4c46e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32906729"
---
# <a name="sqlgetconnectoption-mapping"></a>SQLGetConnectOption 映射
在应用程序调用**SQLGetConnectOption**到 ODBC 3 *.x*驱动程序，将会调用  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 映射，如下所示：  
  
-   如果*fOption*指示返回的字符串，驱动程序管理器调用 ODBC 定义连接选项  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   如果*fOption*指示返回一个 32 位整数值，驱动程序管理器调用 ODBC 定义连接选项  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   如果*fOption*指示驱动程序定义的语句选项，驱动程序管理器调用  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 在前面的三种情况下， *ConnectionHandle*参数设置中的值为*hdbc*、*属性*参数设置中的值为*fOption*，和*ValuePtr*参数设置为相同的值*pvParam*。  
  
 有关 ODBC 定义的字符串连接选项，驱动程序管理器设置*BufferLength*对的调用中的自变量**SQLGetConnectAttr**的预定义的最大长度 (SQL_MAX_OPTION_STRING_LENGTH);对于非字符串连接选项， *BufferLength*设置为 0。  
  
 ODBC 3 *.x*驱动程序，驱动程序管理器不再将检查以查看*选项*SQL_CONN_OPT_MIN 和 SQL_CONN_OPT_MAX，之间或大于 SQL_CONNECT_OPT_DRVR_START。 该驱动程序必须检查选项值的有效性。
