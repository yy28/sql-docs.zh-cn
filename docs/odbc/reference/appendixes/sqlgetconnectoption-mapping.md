---
title: SQLGetConnectOption 映射 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8d2905bd6793d032e485183c8f553cef2cdefda3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301998"
---
# <a name="sqlgetconnectoption-mapping"></a>SQLGetConnectOption 映射
当应用程序通过 ODBC *3.x*驱动程序调用**SQLGetConnectOption**时，调用  
  
```  
SQLGetConnectOption(hdbc, fOption, pvParam)   
```  
  
 映射如下：  
  
-   如果*fOption*指示返回字符串的 ODBC 定义的连接选项，驱动程序管理器将调用  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   如果*fOption*指示一个 ODBC 定义的连接选项，该选项返回 32 位整数值，则驱动程序管理器将调用  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   如果*fOption*指示驱动程序定义的语句选项，则驱动程序管理器将调用  
  
    ```  
    SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 在前面三种情况下 *，ConnectHandle*参数设置为*hdbc*中的值，*属性*参数设置为*fOption*中的值 *，ValuePtr*参数设置为与*pvParam*相同的值。  
  
 对于 ODBC 定义的字符串连接选项，驱动程序管理器在调用**SQLGetConnectAttr**时将*缓冲区长度*参数设置为预定义的最大长度（SQL_MAX_OPTION_STRING_LENGTH）;对于非字符串连接选项，*缓冲区长度*设置为 0。  
  
 对于 ODBC *3.x*驱动程序，驱动程序管理器不再检查*选项*是否位于SQL_CONN_OPT_MIN和SQL_CONN_OPT_MAX之间，还是大于SQL_CONNECT_OPT_DRVR_START。 驱动程序必须检查选项值的有效性。
