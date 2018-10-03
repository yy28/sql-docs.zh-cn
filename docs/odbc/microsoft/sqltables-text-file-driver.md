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
manager: craigg
ms.openlocfilehash: 1299af287d9826893fc8c1f93007967509704d30
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47811865"
---
# <a name="sqltables-text-file-driver"></a>SQLTables（文本文件驱动程序）
> [!NOTE]  
>  本主题提供了文本文件驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|参数|注释|  
|--------------|--------------|  
|*szTableOwner*|唯一有效参数*szTableOwner*为 NULL，因为没有任何驱动程序支持所有者名称。 与*szTableOwner*设置为 NULL，则返回所有表。 在 TABLE_OWNER 列中返回 NULL。|  
|*szTableQualifier*|在 TABLE_QUALIFIER 专栏中， **SQLTables**将返回到目录的路径。|  
|*SzTableType*|"表"是唯一支持的表类型。<br /><br /> 使用文本驱动程序时，返回的文件的列表**SQLTables**由中的文件扩展名**扩展列表**框中**ODBC 文本设置**对话框。|
