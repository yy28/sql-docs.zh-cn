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
manager: craigg
ms.openlocfilehash: f3a3227556a3adfe63431f0cf10169a29d434495
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47653255"
---
# <a name="sqlcolumns-dbase-driver"></a>SQLColumns（dBASE 驱动程序）
> [!NOTE]  
>  本主题提供 dBASE 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|“列”|注释|  
|------------|--------------|  
|TABLE_QUALIFIER|返回到目录的路径。|  
|TABLE_OWNER|在本专栏中则返回 NULL，因为不支持所有者名称。|  
|NULLABLE|SQL_NO_NULLS 主键或唯一索引中的参与的列返回。|
