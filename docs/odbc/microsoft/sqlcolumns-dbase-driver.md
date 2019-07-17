---
title: SQLColumns (dBASE 驱动程序) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5afad2cc08910e036a571e3f32b144bc0b922dda
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132595"
---
# <a name="sqlcolumns-dbase-driver"></a>SQLColumns（dBASE 驱动程序）
> [!NOTE]  
>  本主题提供 dBASE 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|“列”|注释|  
|------------|--------------|  
|TABLE_QUALIFIER|返回到目录的路径。|  
|TABLE_OWNER|在本专栏中则返回 NULL，因为不支持所有者名称。|  
|NULLABLE|SQL_NO_NULLS 主键或唯一索引中的参与的列返回。|
