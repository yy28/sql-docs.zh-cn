---
title: SQLDriverConnect （Access 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Access Driver
ms.assetid: 9d133e9b-7545-464d-aa3c-677fa7e2a41d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a71874c91e48c25072fbfed8f66a312d65b4697
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626376"
---
# <a name="sqldriverconnect-access-driver"></a>SQLDriverConnect（Access 驱动程序）
> [!NOTE]  
>  本主题提供访问特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLDriverConnect**使你能够连接到驱动程序而无需创建数据源 (DSN)。  
  
 在连接字符串中的所有驱动程序支持下列关键字： **DSN**， **DBQ**，并**FIL**。  
  
 **UID**并**PWD**关键字也受支持。  
  
 PWD 关键字不应包含任何特殊字符 (请参阅中的 SQL_SPECIAL_CHARACTERS **SQLGetInfo**返回值)。  
  
 下表显示了连接到每个驱动程序所需的最小关键字并提供与一起使用的关键字/值对的示例**SQLDriverConnect**。 DRIVERID 值的完整列表，请参阅[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。  
  
|驱动程序|所需的关键字|示例|  
|------------|-----------------------|--------------|  
|Microsoft Access|驱动程序 DBQ|驱动程序 = {Microsoft Access 驱动程序 (*.mdb)};DBQ = c:\\\temp\\\sample.mdb|
