---
description: SQLDriverConnect（Paradox 驱动程序）
title: SQLDriverConnect (Paradox 驱动程序) |Microsoft Docs
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
ms.openlocfilehash: 8b6bffe650bfc204660d7345b1bd5a051105fb5b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421811"
---
# <a name="sqldriverconnect-paradox-driver"></a>SQLDriverConnect（Paradox 驱动程序）
> [!NOTE]  
>  本主题提供了特定于驱动程序的信息。 有关此函数的常规信息，请参阅 [ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 **SQLDriverConnect** 使你可以连接到驱动程序，而无需 (DSN) 创建数据源。  
  
 所有驱动程序的连接字符串支持以下关键字： **DSN**、 **DBQ**和 **FIL**。  
  
 还支持 **PWD** 关键字。 PWD 关键字不应包含任何特殊字符 (请参阅 **SQLGetInfo** 返回值) 中 SQL_SPECIAL_CHARACTERS。  
  
 用户打开了受密码保护的文件后，不允许其他用户打开同一文件。  
  
 下表显示连接到每个驱动程序所需的最小关键字，并提供用于 **SQLDriverConnect**的关键字/值对的示例。 有关 DRIVERID 值的完整列表，请参阅 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-paradox-driver.md)。  
  
> [!NOTE]  
>  如果未指定 Paradox 驱动程序的 DBQ 或 DefaultDir，则驱动程序将连接到当前目录。  
  
|驱动程序|需要关键字|示例|  
|------------|-----------------------|-------------|  
|Paradox|驱动程序，DriverID|Driver = {Microsoft Paradox Driver ( * .db ) };DBQ = c：\temp; DriverID = 26|
