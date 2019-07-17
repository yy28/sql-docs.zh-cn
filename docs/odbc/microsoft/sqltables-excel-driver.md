---
title: SQLTables （Excel 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 89157178aa9c134bdb1b9518343007adb1e1e05f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132416"
---
# <a name="sqltables-excel-driver"></a>SQLTables（Excel 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 Excel 驱动程序的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|参数|注释|  
|--------------|--------------|  
|*szTableOwner*|唯一有效参数*szTableOwner*为 NULL，因为没有任何驱动程序支持所有者名称。 与*szTableOwner*设置为 NULL，则返回所有表。 在 TABLE_OWNER 列中返回 NULL。|  
|*szTableQualifier*|Microsoft Excel 3.0 或 4.0 版驱动程序使用时，如果您调用**SQLTables**的值与*szTableQualifier*的不是现有表的名称，该驱动程序将具有该名称创建一个表。<br /><br /> 在 TABLE_QUALIFIER 专栏中， **SQLTables**将返回到目录的路径。|  
|*SzTableType*|对于 Microsoft Excel 3.0 或 4.0，"表"是唯一支持的表类型。<br /><br /> 更高版本的 Microsoft Excel 文件中，"系统表"返回的表名称 （以"$"端上的表），并为工作表中的表返回"TABLE"。|
