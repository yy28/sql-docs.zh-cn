---
title: SQLTables（可视化福克斯Pro ODBC驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5467fc8c1717d5ceb548b3950a0894fd2a1b4499
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299278"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持： 完整  
  
 ODBC API 符合性：1 级  
  
 返回**SQLTables**语句中参数指定的表名称的列表。 如果未指定参数，则返回存储在当前数据源中的表名称。 驱动程序将返回结果集。  
  
 枚举类型调用将不会接收远程视图或本地参数化视图的结果集条目。 但是，如果存在具有该名称的**SQLTables，** 则使用唯一表名称指定器的调用将找到此类视图的匹配项;这允许在创建新表之前使用 API 检查名称冲突。  
  
> [!NOTE]  
>  Visual FoxPro ODBC 驱动程序区分[数据库表](../../odbc/microsoft/visual-foxpro-terminology.md)和[可用表](../../odbc/microsoft/visual-foxpro-terminology.md)，即使这两种类型的表都存储在系统上的同一目录中。 如果数据源是可用表的目录，则 Visual FoxPro ODBC 驱动程序不会编目或返回与数据库关联的任何表的名称。  
  
 有关详细信息，请参阅*ODBC 程序员参考中的* [SQLTables。](../../odbc/reference/syntax/sqltables-function.md)
