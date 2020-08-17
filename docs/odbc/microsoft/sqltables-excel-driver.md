---
description: SQLTables（Excel 驱动程序）
title: SQLTables (Excel 驱动程序) |Microsoft Docs
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
ms.openlocfilehash: acedd48fb48e8f8db844feb1911f044c472006a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339643"
---
# <a name="sqltables-excel-driver"></a>SQLTables（Excel 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 Excel 驱动程序的信息。 有关此函数的常规信息，请参阅 [ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
|参数|注释|  
|--------------|--------------|  
|*szTableOwner*|*SzTableOwner*的唯一有效参数是 NULL，因为这些驱动程序都不支持所有者名称。 如果 *szTableOwner* 设置为 NULL，则返回所有表。 在 TABLE_OWNER 列中返回 NULL。|  
|*szTableQualifier*|当使用 Microsoft Excel 3.0 或4.0 驱动程序时，如果使用不是现有表的名称的*szTableQualifier*值调用**SQLTables** ，则驱动程序将创建具有该名称的表。<br /><br /> 在 TABLE_QUALIFIER 列中， **SQLTables** 将返回目录的路径。|  
|*SzTableType*|对于 Microsoft Excel 3.0 或4.0，"表" 是唯一受支持的表类型。<br /><br /> 对于更高版本的 Microsoft Excel 文件，将为工作表名称返回 "系统表"， (表中的 "$" 作为结束) ，并为工作表中的表返回 "表"。|
