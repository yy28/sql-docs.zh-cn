---
title: SQLTables（Excel 驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLTables
- SQLTables function [ODBC], Excel Driver
ms.assetid: 9410b686-4b5b-4b51-b5ef-f9d2e7a48faa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c436a1f52a862cda753d8c043515f5584607d98c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299297"
---
# <a name="sqltables-excel-driver"></a>SQLTables（Excel 驱动程序）
> [!NOTE]  
>  本主题提供特定于 Excel 驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
|参数|注释|  
|--------------|--------------|  
|*szTable 所有者*|*szTableOwner*的唯一有效参数是 NULL，因为没有任何驱动程序支持所有者名称。 将*szTableOwner*设置为 NULL 时，将返回所有表。 NULL 在TABLE_OWNER列中返回。|  
|*szTable限定符*|使用 Microsoft Excel 3.0 或 4.0 驱动程序时，如果调用**SQLTable**的值为*szTableQualifier，* 而不是现有表的名称，则驱动程序将创建具有该名称的表。<br /><br /> 在TABLE_QUALIFIER列中 **，SQLTables**将路径返回到目录。|  
|*SzTable 类型*|对于 Microsoft Excel 3.0 或 4.0，"TABLE"是唯一支持的表类型。<br /><br /> 对于更高版本的 Microsoft Excel 文件，对于工作表名称（末尾有"$"的表）返回"SYSTEM TABLE"，对于工作表中的表返回"TABLE"。|
