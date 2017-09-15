---
title: "SQLColumns (dBASE 驱动程序) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLColumns function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLColumns
ms.assetid: 168171de-ab7d-4b5b-af7f-6e2106adfcce
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a55f12a84c6fb354b4aefa4da40c53473cd4b215
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolumns-dbase-driver"></a>SQLColumns (dBASE 驱动程序)
> [!NOTE]  
>  本主题提供 dBASE 特定于驱动程序的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|列|注释|  
|------------|--------------|  
|TABLE_QUALIFIER|返回到目录的路径。|  
|TABLE_OWNER|因为不支持所有者名称，将在此列中返回 NULL。|  
|NULLABLE|SQL_NO_NULLS 针对参与的列返回中的主键或唯一索引。|
