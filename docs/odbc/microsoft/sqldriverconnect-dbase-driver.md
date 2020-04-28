---
title: SQLDriverConnect （dBASE 驱动程序） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302918"
---
# <a name="sqldriverconnect-dbase-driver"></a>SQLDriverConnect（dBASE 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 dBASE 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 **SQLDriverConnect**使你能够连接到驱动程序，而无需创建数据源（DSN）。  
  
 所有驱动程序的连接字符串支持以下关键字： **DSN**、 **DBQ**和**FIL**。  
  
 使用 Paradox 驱动程序时，如果用户打开了密码保护的文件，则不允许其他用户打开同一文件。  
  
 下表显示连接到每个驱动程序所需的最小关键字，并提供用于**SQLDriverConnect**的关键字/值对的示例。 有关 DRIVERID 值的完整列表，请参阅[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)。  
  
> [!NOTE]  
>  如果没有为 dBASEdriver 指定 DBQ 或 DefaultDir，则驱动程序将连接到当前目录。  
  
|驱动程序|需要关键字|示例|  
|------------|-----------------------|--------------|  
|dBASE|驱动程序，DriverID|Driver = {Microsoft dBASE 驱动程序（* .dbf）};DBQ = c：\temp;DriverID = 277|
