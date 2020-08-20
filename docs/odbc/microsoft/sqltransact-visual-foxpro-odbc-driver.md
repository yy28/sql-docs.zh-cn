---
description: SQLTransact（Visual FoxPro ODBC 驱动程序）
title: SQLTransact (Visual FoxPro ODBC 驱动程序) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTransact function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 92cf86c0-f7a8-44d7-b59f-a1342677440b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1deed379c456ba2f15d30b6783c95d657e688457
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500110"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅 [ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：核心级别  
  
 为所有语句句柄上的所有活动操作请求提交或回滚操作，该操作将 (*hstmt*s) 与连接相关联，或用于与环境句柄 *henv*关联的所有连接。 **SQLTransact** 仅适用于作为 [数据库](../../odbc/microsoft/visual-foxpro-terminology.md)的数据源。  
  
 如果在手动模式下提交失败，则事务将保持活动状态;您可以选择回滚事务或重试提交操作。 如果在自动事务模式下提交操作失败，则将自动回滚事务;该事务不能处于非活动状态。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLTransact](../../odbc/reference/syntax/sqltransact-function.md) 。
