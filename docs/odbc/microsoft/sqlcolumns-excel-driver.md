---
title: SQLColumns （Excel 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8481a4ea9cf69b615aa0142cc01556018801e823
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132542"
---
# <a name="sqlcolumns-excel-driver"></a>SQLColumns（Excel 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 Excel 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
|列|注释|  
|------------|--------------|  
|TABLE_QUALIFIER|返回目录的路径。|  
|TABLE_OWNER|由于不支持所有者名称，因此在此列中返回 NULL。|  
|NULLABLE|对于参与主键或唯一索引的列，将返回 SQL_NO_NULLS。|
