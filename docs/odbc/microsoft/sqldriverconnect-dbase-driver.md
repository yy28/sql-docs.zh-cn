---
title: SQLDriver连接（dBASE驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], dBASE Driver
ms.assetid: c837aa31-068e-4fa3-bc00-aae09bec21de
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39d3d062ef8371ce37f812216cbb642d103eff98
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302918"
---
# <a name="sqldriverconnect-dbase-driver"></a>SQLDriverConnect（dBASE 驱动程序）
> [!NOTE]  
>  本主题提供特定于 dBASE 驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 **SQLDriverConnect**使您能够连接到驱动程序，而无需创建数据源 （DSN）。  
  
 所有驱动程序的连接字符串都支持以下关键字 **：DSN、DBQ**和**DBQ****FIL**。  
  
 使用 Paradox 驱动程序时，用户打开受密码保护的文件后，不允许其他用户打开同一文件。  
  
 下表显示了连接到每个驱动程序所需的最小关键字，并提供了**SQLDriverConnect**一起使用的关键字/值对的示例。 有关 DRIVERID 值的完整列表，请参阅[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。  
  
> [!NOTE]  
>  如果未为 dBASEdriver 指定 DBQ 或 DefaultDir，则驱动程序将连接到当前目录。  
  
|驱动程序|所需的关键字|示例|  
|------------|-----------------------|--------------|  
|dBASE|驱动程序，驱动程序 ID|驱动程序[微软 dBASE 驱动程序 （*.dbf）];DBQ_c：\temp;驱动程序 ID=277|
