---
title: SQLColumns （dBASE 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColumns function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLColumns
ms.assetid: 168171de-ab7d-4b5b-af7f-6e2106adfcce
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 242e4c2c95340aaf8bd4a8d8d41959b388a1cf70
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307888"
---
# <a name="sqlcolumns-dbase-driver"></a>SQLColumns（dBASE 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 dBASE 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
|列|说明|  
|------------|--------------|  
|TABLE_QUALIFIER|返回目录的路径。|  
|TABLE_OWNER|由于不支持所有者名称，因此在此列中返回 NULL。|  
|NULLABLE|对于参与主键或唯一索引的列，将返回 SQL_NO_NULLS。|
