---
title: "SQLDriverConnect （Access 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Access driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Access Driver
ms.assetid: 9d133e9b-7545-464d-aa3c-677fa7e2a41d
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a43805d014324e068943d61c000461e3f64c2ebf
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqldriverconnect-access-driver"></a>SQLDriverConnect （Access 驱动程序）
> [!NOTE]  
>  本主题提供访问特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLDriverConnect**使你能够连接到的驱动程序而无需创建数据源 (DSN)。  
  
 在连接字符串中的所有驱动程序支持以下关键字： **DSN**， **DBQ**，和**FIL**。  
  
 **UID**和**PWD**关键字也支持。  
  
 PWD 关键字不应包含任何特殊字符 (请参阅中的 SQL_SPECIAL_CHARACTERS **SQLGetInfo**返回值)。  
  
 下表显示了连接到每个驱动程序，所需的最小关键字并提供了与使用的关键字/值对的一个示例**SQLDriverConnect**。 DRIVERID 值的完整列表，请参阅[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。  
  
|驱动程序|所需的关键字|示例|  
|------------|-----------------------|--------------|  
|Microsoft Access|驱动程序 DBQ|驱动程序 = {Microsoft Access 驱动程序 (*.mdb)};DBQ = c:\\\temp\\\sample.mdb|
