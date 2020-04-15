---
title: SQLDriver连接（悖论驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68171cfab2b65634433b107d829dd2a6e9b5c985
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307108"
---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect（Paradox 驱动程序）
> [!NOTE]  
>  本主题提供特定于悖论驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 **SQLDriverConnect**使您能够连接到驱动程序，而无需创建数据源 （DSN）。  
  
 所有驱动程序的连接字符串都支持以下关键字 **：DSN、DBQ**和**DBQ****FIL**。  
  
 **PWD**关键字也受支持。 PWD 关键字不应包含任何特殊字符（请参阅**SQLGetInfo**返回值中的SQL_SPECIAL_CHARACTERS）。  
  
 用户打开受密码保护的文件后，不允许其他用户打开同一文件。  
  
 下表显示了连接到每个驱动程序所需的最小关键字，并提供了**SQLDriverConnect**一起使用的关键字/值对的示例。 有关 DRIVERID 值的完整列表，请参阅[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。  
  
> [!NOTE]  
>  如果未为 Paradox 驱动程序指定 DBQ 或 DefaultDir，则驱动程序将连接到当前目录。  
  
|驱动程序|所需的关键字|示例|  
|------------|-----------------------|-------------|  
|悖论|驱动程序，驱动程序 ID|驱动程序=微软悖论驱动程序 （*.db ）;=DBQ_c：\temp;驱动程序 ID=26|
