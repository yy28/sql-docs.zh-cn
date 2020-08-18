---
description: SQLDriverConnect（Access 驱动程序）
title: SQLDriverConnect (Access 驱动程序) |Microsoft Docs
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
ms.openlocfilehash: 52bbcbfa379be53ea24c150d2522242e85e61fea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449209"
---
# <a name="sqldriverconnect-access-driver"></a>SQLDriverConnect（Access 驱动程序）
> [!NOTE]  
>  本主题提供特定于访问驱动程序的信息。 有关此函数的常规信息，请参阅 [ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 **SQLDriverConnect** 使你可以连接到驱动程序，而无需 (DSN) 创建数据源。  
  
 所有驱动程序的连接字符串支持以下关键字： **DSN**、 **DBQ**和 **FIL**。  
  
 还支持 **UID** 和 **PWD** 关键字。  
  
 PWD 关键字不应包含任何特殊字符 (请参阅 **SQLGetInfo** 返回值) 中 SQL_SPECIAL_CHARACTERS。  
  
 下表显示连接到每个驱动程序所需的最小关键字，并提供用于 **SQLDriverConnect**的关键字/值对的示例。 有关 DRIVERID 值的完整列表，请参阅 [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)。  
  
|驱动程序|需要关键字|示例|  
|------------|-----------------------|--------------|  
|Microsoft Access|驱动程序，DBQ|Driver = {Microsoft Access Driver ( * .mdb) };DBQ = c： \\ \temp \\ \sample.mdb|
