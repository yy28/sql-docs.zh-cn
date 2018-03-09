---
title: "SQLTables （Visual FoxPro ODBC 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLTables function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 69e2a038-5def-423f-91aa-8756e069dd2a
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 75a251ab1c392b1a351ee36c39fe340f2122c610
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables （Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序相关的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 完整  
  
 ODBC API 一致性： 级别 1  
  
 返回由参数中指定的表名称的列表**SQLTables**语句。 如果未不指定任何参数，则返回当前的数据源中存储的表名称。 驱动程序返回信息作为结果集。  
  
 枚举类型调用不会收到远程视图或本地的参数化的视图的结果集条目。 但是，对的调用**SQLTables**使用唯一表名称说明符会发现这样的视图的匹配项如果存在具有该名称; 这使得此 API 可以用于检查之前创建的新表的名称冲突。  
  
> [!NOTE]  
>  Visual FoxPro ODBC 驱动程序可区分[数据库表](../../odbc/microsoft/visual-foxpro-terminology.md)和[释放表](../../odbc/microsoft/visual-foxpro-terminology.md)，即使当你的系统上的相同目录中存储两种类型的表。 如果您的数据源是可用的表的目录，Visual FoxPro ODBC 驱动程序不目录或不返回任何与数据库相关联的表的名称。  
  
 有关详细信息，请参阅[SQLTables](../../odbc/reference/syntax/sqltables-function.md)中*ODBC 程序员参考*。
