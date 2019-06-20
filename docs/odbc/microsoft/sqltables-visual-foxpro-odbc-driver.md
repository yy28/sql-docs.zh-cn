---
title: SQLTables （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e134b2870c4506e725f2900b83d1118e42b55d15
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63219122"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持：完全  
  
 ODBC API 一致性：级别 1  
  
 返回由参数中指定的表名称的列表**SQLTables**语句。 如果未不指定任何参数，将返回当前的数据源中存储的表名称。 驱动程序返回的信息作为结果集。  
  
 枚举类型调用不会收到远程视图或本地的参数化的视图的结果集条目。 但是，调用**SQLTables**使用唯一表名称说明符会发现这样的视图的匹配项如果存在具有该名称; 这使得此 API 可以用于检查创建的新表之前的名称冲突。  
  
> [!NOTE]  
>  Visual FoxPro ODBC 驱动程序区分[数据库表](../../odbc/microsoft/visual-foxpro-terminology.md)并[免费表](../../odbc/microsoft/visual-foxpro-terminology.md)，即使这两种类型的表存储在您的系统上的同一目录中。 如果您的数据源的可用表的目录，Visual FoxPro ODBC 驱动程序不目录或不返回任何与数据库相关联的表的名称。  
  
 有关详细信息，请参阅[SQLTables](../../odbc/reference/syntax/sqltables-function.md)中*ODBC 程序员参考*。
