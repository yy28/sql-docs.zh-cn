---
description: SQLFreeConnect 映射
title: SQLFreeConnect 映射 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], SQLFreeConnect
- SQLFreeConnect function [ODBC], mapping
ms.assetid: 8a844538-93c0-4709-bab6-35c45e771d80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ad5c2e5b1f519986ec59535699320aa8c11595c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461629"
---
# <a name="sqlfreeconnect-mapping"></a>SQLFreeConnect 映射
当应用程序*通过 ODBC 1.x*驱动程序调用**SQLFreeConnect**时，调用  
  
```  
SQLFreeConnect(hdbc)   
```  
  
 映射到  
  
```  
SQLFreeHandle(SQL_HANDLE_DBC,Handle)  
```  
  
 如果将 *Handle* 参数设置为 *hdbc*中的值，则为。
