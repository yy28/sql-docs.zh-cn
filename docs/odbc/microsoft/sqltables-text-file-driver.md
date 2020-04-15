---
title: SQLTables（文本文件驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 938ceba5da25d176628d5c1d9875383d977e3aec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299327"
---
# <a name="sqltables-text-file-driver"></a>SQLTables（文本文件驱动程序）
> [!NOTE]  
>  本主题提供特定于文本文件驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
|参数|注释|  
|--------------|--------------|  
|*szTable 所有者*|*szTableOwner*的唯一有效参数是 NULL，因为没有任何驱动程序支持所有者名称。 将*szTableOwner*设置为 NULL 时，将返回所有表。 NULL 在TABLE_OWNER列中返回。|  
|*szTable限定符*|在TABLE_QUALIFIER列中 **，SQLTables**将路径返回到目录。|  
|*SzTable 类型*|"TABLE"是唯一支持的表类型。<br /><br /> 使用文本驱动程序时 **，SQLTables**返回的文件列表由**ODBC 文本设置**对话框中的 **"扩展列表"** 框中的文件扩展名确定。|
