---
title: SQLTables （文本文件驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLTables
- SQLTables function [ODBC], Text File Driver
ms.assetid: f47fd1a4-5bd8-4b2e-8ae3-e595e49f4f95
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7fcdf9cc41a55d1e529001ae7183ef9fa833363b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949017"
---
# <a name="sqltables-text-file-driver"></a>SQLTables（文本文件驱动程序）
> [!NOTE]  
>  本主题提供特定于文本文件驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
|参数|注释|  
|--------------|--------------|  
|*szTableOwner*|*SzTableOwner*的唯一有效参数是 NULL，因为这些驱动程序都不支持所有者名称。 如果*szTableOwner*设置为 NULL，则返回所有表。 在 TABLE_OWNER 列中返回 NULL。|  
|*szTableQualifier*|在 TABLE_QUALIFIER 列中， **SQLTables**将返回目录的路径。|  
|*SzTableType*|"TABLE" 是唯一受支持的表类型。<br /><br /> 使用文本驱动程序时，由**SQLTables**返回的文件列表由 " **ODBC 文本设置**" 对话框中的 "**扩展" 列表**框中的文件扩展名确定。|
