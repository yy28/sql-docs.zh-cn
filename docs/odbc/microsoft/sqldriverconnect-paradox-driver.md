---
title: SQLDriverConnect （Paradox 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLDriverConnect
ms.assetid: c2ba486e-5e01-4e67-adb1-68511f5f0206
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bae4a842729c8d302731ebf5fec22abb817f4c75
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654755"
---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect（Paradox 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 Paradox 驱动程序的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLDriverConnect**使你能够连接到驱动程序而无需创建数据源 (DSN)。  
  
 在连接字符串中的所有驱动程序支持下列关键字： **DSN**， **DBQ**，并**FIL**。  
  
 **PWD**还支持关键字。 PWD 关键字不应包含任何特殊字符 (请参阅中的 SQL_SPECIAL_CHARACTERS **SQLGetInfo**返回值)。  
  
 由用户打开受密码保护的文件后，不允许其他用户打开同一文件。  
  
 下表显示了连接到每个驱动程序所需的最小关键字并提供与一起使用的关键字/值对的示例**SQLDriverConnect**。 DRIVERID 值的完整列表，请参阅[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。  
  
> [!NOTE]  
>  如果没有为 Paradox 驱动程序指定 DBQ 或 DefaultDir，驱动程序将连接到当前目录中。  
  
|驱动程序|所需的关键字|示例|  
|------------|-----------------------|-------------|  
|Paradox|驱动程序 DriverID|Driver={Microsoft Paradox Driver (*.db )}; DBQ=c:\temp;DriverID=26|
