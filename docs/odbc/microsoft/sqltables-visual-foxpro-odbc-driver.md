---
description: SQLTables（Visual FoxPro ODBC 驱动程序）
title: SQLTables (Visual FoxPro ODBC 驱动程序) |Microsoft Docs
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
ms.openlocfilehash: 089208ab612984283e3f87c4ad03aca0ccfa2b38
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471549"
---
# <a name="sqltables-visual-foxpro-odbc-driver"></a>SQLTables（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅 [ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：级别1  
  
 返回由 **SQLTables** 语句中的参数指定的表名称的列表。 如果未指定参数，则返回存储在当前数据源中的表名。 驱动程序将以结果集的形式返回该信息。  
  
 枚举类型调用不会接收远程视图或本地参数化视图的结果集条目。 但是，如果使用唯一的表名称说明符调用 **SQLTables** ，则会找到此类视图的匹配项（如果存在同名的视图）;这允许在创建新表之前使用 API 检查名称冲突。  
  
> [!NOTE]  
>  Visual FoxPro ODBC 驱动程序在 [数据库表](../../odbc/microsoft/visual-foxpro-terminology.md) 和 [可用表](../../odbc/microsoft/visual-foxpro-terminology.md)之间区分开来，即使两种类型的表都存储在系统的同一目录中。 如果数据源是可用表的一个目录，则 Visual FoxPro ODBC 驱动程序不会对与数据库关联的任何表的名称进行分类或返回。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLTables](../../odbc/reference/syntax/sqltables-function.md) 。
