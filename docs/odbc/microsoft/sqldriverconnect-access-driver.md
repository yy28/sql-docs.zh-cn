---
title: SQLDriver连接（访问驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a679cbb16ece3f239b1d17daabc8a294b808287
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302908"
---
# <a name="sqldriverconnect-access-driver"></a>SQLDriverConnect（Access 驱动程序）
> [!NOTE]  
>  本主题提供特定于访问驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 **SQLDriverConnect**使您能够连接到驱动程序，而无需创建数据源 （DSN）。  
  
 所有驱动程序的连接字符串都支持以下关键字 **：DSN、DBQ**和**DBQ****FIL**。  
  
 也支持**UID**和**PWD**关键字。  
  
 PWD 关键字不应包含任何特殊字符（请参阅**SQLGetInfo**返回值中的SQL_SPECIAL_CHARACTERS）。  
  
 下表显示了连接到每个驱动程序所需的最小关键字，并提供了**SQLDriverConnect**一起使用的关键字/值对的示例。 有关 DRIVERID 值的完整列表，请参阅[SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。  
  
|驱动程序|所需关键字|示例|  
|------------|-----------------------|--------------|  
|Microsoft Access|驱动程序，DBQ|驱动程序[微软访问驱动程序 （*.mdb）];DBQ_c：\\\temp\\_sample.mdb|
