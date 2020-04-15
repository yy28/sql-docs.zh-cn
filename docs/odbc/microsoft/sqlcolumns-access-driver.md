---
title: SQL柱（访问驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColumns function [ODBC], Access Driver
- Access driver [ODBC], SQLColumns
ms.assetid: 1eac255c-6110-4805-a1bc-feee1eec35d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7031e9eebbb1ffae045598863d22399147503c88
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307898"
---
# <a name="sqlcolumns-access-driver"></a>SQLColumns（Access 驱动程序）
> [!NOTE]  
>  本主题提供特定于访问驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
|列|注释|  
|------------|--------------|  
|TABLE_QUALIFIER|返回数据库文件的路径。|  
|TABLE_OWNER|由于不支持所有者名称，因此在此列中返回 NULL。|  
|NULLABLE|对于参与主键或唯一索引的列，将返回SQL_NO_NULLS。|
