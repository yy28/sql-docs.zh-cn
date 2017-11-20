---
title: "SQLColumns （文本文件驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], SQLColumns
- SQLColumns function [ODBC], Text File Driver
ms.assetid: c99e5f8d-4e43-48f8-9e0e-086707b411f5
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a5f64eb930bad551953c4a70b2d839924d127caf
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolumns-text-file-driver"></a>SQLColumns （文本文件驱动程序）
> [!NOTE]  
>  本主题提供文本文件特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|列|注释|  
|------------|--------------|  
|TABLE_QUALIFIER|返回到目录的路径。|  
|TABLE_OWNER|因为不支持所有者名称，将在此列中返回 NULL。|  
|NULLABLE|SQL_NO_NULLS 针对参与的列返回中的主键或唯一索引。|

