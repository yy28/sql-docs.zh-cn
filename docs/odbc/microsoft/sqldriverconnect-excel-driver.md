---
title: "SQLDriverConnect （Excel 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Excel driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Excel Driver
ms.assetid: 285cb1ea-f461-4596-97f2-fc57af05dede
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eca660cf2c38539dbf4a0fa560bfc67a1b1be115
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect （Excel 驱动程序）
> [!NOTE]  
>  本主题提供 Excel 驱动程序相关的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 **SQLDriverConnect**使你能够连接到的驱动程序而无需创建数据源 (DSN)。  
  
 在连接字符串中的所有驱动程序支持以下关键字： **DSN**， **DBQ**，和**FIL**。  
  
 下表显示了连接到每个驱动程序，所需的最小关键字并提供了与使用的关键字/值对的一个示例**SQLDriverConnect**。 DRIVERID 值的完整列表，请参阅[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。  
  
> [!NOTE]  
>  如果没有为 Microsoft Excel 3.0 或 4.0 驱动程序指定 DBQ 或 DefaultDir，驱动程序将连接到当前目录中。  
  
|驱动程序|所需的关键字|示例|  
|------------|-----------------------|--------------|  
|Microsoft Excel 3.0 或 4.0|驱动程序 DriverID|驱动程序 = {Microsoft Excel 驱动程序 (*.xls)};DBQ = c:\temp;DriverID = 278|  
|Microsoft Excel 5.0/7.0|驱动程序，DriverID DBQ|驱动程序 = {Microsoft Excel 驱动程序 (*.xls)};DBQ=c:\temp\sample.xls;DriverID = 22|  
|Microsoft Excel 97 及更高版本|驱动程序，DriverID DBQ|驱动程序 = {Microsoft Excel 驱动程序 (*.xls)};DBQ=c:\temp\sample.xls;DriverID = 790|

