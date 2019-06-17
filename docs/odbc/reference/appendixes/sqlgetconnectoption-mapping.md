---
title: SQLGetConnectOption Mapping | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLGetConnectOption
- SQLGetConnectOption function [ODBC], mapping
ms.assetid: e3792fe4-a955-473a-a297-c1b2403660c4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8504709cb2cedb36c62bb9be74ffc8d12a4c811d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188786"
---
# <a name="sqlgetconnectoption-mapping"></a>SQLGetConnectOption 映射
当应用程序调用**SQLGetConnectOption**通过 ODBC 3 *.x*驱动程序，将会调用  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 映射，如下所示：  
  
-   如果*fOption*指示返回的字符串，该驱动程序管理器调用一个 ODBC 定义的连接选项  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   如果*fOption*指示返回 32 位整数值，驱动程序管理器调用一个 ODBC 定义的连接选项  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   如果*fOption*指示驱动程序定义的语句选项，驱动程序管理器调用  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 在前面的三种情况下， *ConnectionHandle*参数设置为中的值*hdbc*，则*特性*参数设置中的值为*fOption*，并*ValuePtr*参数设置为相同的值*pvParam*。  
  
 有关 ODBC 定义的字符串连接选项，驱动程序管理器设置*BufferLength*调用中的参数**SQLGetConnectAttr**为预定义的最大长度 (SQL_MAX_OPTION_STRING_LENGTH);对于非字符串连接选项，请*BufferLength*设置为 0。  
  
 对于 ODBC 3 *.x*驱动程序，驱动程序管理器不再检查以查看是否*选项*介于 SQL_CONN_OPT_MIN 和 SQL_CONN_OPT_MAX，或者大于 SQL_CONNECT_OPT_DRVR_START。 该驱动程序必须检查的选项值的有效性。
