---
title: SQL柱（Excel 驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColumns function [ODBC], Excel Driver
- Excel driver [ODBC], SQLColumns
ms.assetid: 4bae3fcd-0287-4f79-ad7c-8f7ab2f6f940
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c168168e0cb44d6aff2102bb18c07cbf1a1953a5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307878"
---
# <a name="sqlcolumns-excel-driver"></a>SQLColumns（Excel 驱动程序）
> [!NOTE]  
>  本主题提供特定于 Excel 驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
|列|注释|  
|------------|--------------|  
|TABLE_QUALIFIER|返回目录的路径。|  
|TABLE_OWNER|由于不支持所有者名称，因此在此列中返回 NULL。|  
|NULLABLE|对于参与主键或唯一索引的列，将返回SQL_NO_NULLS。|
