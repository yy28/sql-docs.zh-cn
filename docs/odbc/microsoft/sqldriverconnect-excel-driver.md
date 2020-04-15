---
title: SQLDriver连接（Excel驱动程序） |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307118"
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect（Excel 驱动程序）
> [!NOTE]  
>  本主题提供特定于 Excel 驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 **SQLDriverConnect**使您能够连接到驱动程序，而无需创建数据源 （DSN）。  
  
 所有驱动程序的连接字符串都支持以下关键字 **：DSN、DBQ**和**DBQ****FIL**。  
  
 下表显示了连接到每个驱动程序所需的最小关键字，并提供了**SQLDriverConnect**一起使用的关键字/值对的示例。 有关 DRIVERID 值的完整列表，请参阅[SQLConfigDataSource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)。  
  
> [!NOTE]  
>  如果未为 Microsoft Excel 3.0 或 4.0 驱动程序指定 DBQ 或 DefaultDir，则驱动程序将连接到当前目录。  
  
|驱动程序|所需关键字|示例|  
|------------|-----------------------|--------------|  
|微软 Excel 3.0 或 4.0|驱动程序，驱动程序 ID|驱动程序[微软 Excel 驱动程序 （*.xls）];DBQ_c：\temp;驱动程序 ID=278|  
|微软 Excel 5.0/7.0|驱动程序、驱动程序 ID、DBQ|驱动程序[微软 Excel 驱动程序 （*.xls）];DBQ_c：\temp_sample.xls;驱动程序 ID=22|  
|微软 Excel 97 及更高版本|驱动程序、驱动程序 ID、DBQ|驱动程序[微软 Excel 驱动程序 （*.xls）];DBQ_c：\temp_sample.xls;驱动程序 ID=790|
