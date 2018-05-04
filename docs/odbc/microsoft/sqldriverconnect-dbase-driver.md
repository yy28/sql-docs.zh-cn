---
title: SQLDriverConnect (dBASE 驱动程序) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], dBASE Driver
ms.assetid: c837aa31-068e-4fa3-bc00-aae09bec21de
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7fe97e7c3541a86119459ba4c65ee247d06b96ac
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqldriverconnect-dbase-driver"></a>SQLDriverConnect (dBASE 驱动程序)
> [!NOTE]  
>  本主题提供 dBASE 特定于驱动程序的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLDriverConnect**使你能够连接到的驱动程序而无需创建数据源 (DSN)。  
  
 在连接字符串中的所有驱动程序支持以下关键字： **DSN**， **DBQ**，和**FIL**。  
  
 当使用 Paradox 驱动程序时，而用户打开受密码保护的文件后时，不允许其他用户打开相同的文件。  
  
 下表显示了连接到每个驱动程序，所需的最小关键字并提供了与使用的关键字/值对的一个示例**SQLDriverConnect**。 DRIVERID 值的完整列表，请参阅[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。  
  
> [!NOTE]  
>  如果没有为 dBASEdriver 指定 DBQ 或 DefaultDir，驱动程序将连接到当前目录中。  
  
|驱动程序|所需的关键字|示例|  
|------------|-----------------------|--------------|  
|dBASE|驱动程序 DriverID|Driver={Microsoft dBASE Driver (*.dbf)}; DBQ=c:\temp; DriverID=277|
