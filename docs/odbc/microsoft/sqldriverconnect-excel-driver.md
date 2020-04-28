---
title: SQLDriverConnect （Excel 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Excel Driver
ms.assetid: 285cb1ea-f461-4596-97f2-fc57af05dede
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1108206bf38183887540b114fda5a1e913aa67d9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307118"
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect（Excel 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 Excel 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 **SQLDriverConnect**使你能够连接到驱动程序，而无需创建数据源（DSN）。  
  
 所有驱动程序的连接字符串支持以下关键字： **DSN**、 **DBQ**和**FIL**。  
  
 下表显示连接到每个驱动程序所需的最小关键字，并提供用于**SQLDriverConnect**的关键字/值对的示例。 有关 DRIVERID 值的完整列表，请参阅[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。  
  
> [!NOTE]  
>  如果未指定 Microsoft Excel 3.0 或4.0 驱动程序的 DBQ 或 DefaultDir，则驱动程序将连接到当前目录。  
  
|驱动程序|需要关键字|示例|  
|------------|-----------------------|--------------|  
|Microsoft Excel 3.0 或4。0|驱动程序，DriverID|Driver = {Microsoft Excel 驱动程序（* .xls）};DBQ = c：\temp;DriverID = 278|  
|Microsoft Excel 5.0/7。0|Driver、DriverID、DBQ|Driver = {Microsoft Excel 驱动程序（* .xls）};DBQ = c:\temp\sample.xls;DriverID = 22|  
|Microsoft Excel 97 及更高版本|Driver、DriverID、DBQ|Driver = {Microsoft Excel 驱动程序（* .xls）};DBQ = c:\temp\sample.xls;DriverID = 790|
