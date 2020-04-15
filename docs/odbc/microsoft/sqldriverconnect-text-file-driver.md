---
title: SQLDriver连接（文本文件驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLDriverConnect function [ODBC], Text File Driver
- text file driver [ODBC], SQLDriverConnect
ms.assetid: d7769021-bd18-4d8e-96e0-e184a82d6ca3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2768669b7dbb2066de0acedd5711911be0eac8fa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307098"
---
# <a name="sqldriverconnect-text-file-driver"></a>SQLDriverConnect（文本文件驱动程序）
> [!NOTE]  
>  本主题提供特定于文本文件驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 **SQLDriverConnect**使您能够连接到驱动程序，而无需创建数据源 （DSN）。  
  
 所有驱动程序的连接字符串都支持以下关键字 **：DSN、DBQ**和**DBQ****FIL**。  
  
 下表显示了连接到每个驱动程序所需的最小关键字，并提供了**SQLDriverConnect**一起使用的关键字/值对的示例。 有关 DRIVERID 值的完整列表，请参阅[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-text-file-driver.md)。  
  
> [!NOTE]  
>  如果未为文本驱动程序指定 DBQ 或 DefaultDir，则驱动程序将连接到当前目录。  
  
|驱动程序|所需的关键字|示例|  
|------------|-----------------------|--------------|  
|Text|驱动程序|驱动程序\微软文本驱动程序 （*.txt;\*.csv）*;默认 Dir_c：\temp|
