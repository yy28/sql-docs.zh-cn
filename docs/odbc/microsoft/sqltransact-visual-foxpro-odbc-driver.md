---
title: SQLTransact （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e554a8669b6e6e95e234a5b939477a8bb2f7b8cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948869"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持：完全  
  
 ODBC API 一致性：核心级别  
  
 请求的所有语句句柄上的所有活动操作提交或回滚操作 (*hstmt*s) 与连接或适用于所有环境句柄，与关联的连接关联*henv*。 **SQLTransact**仅适用于数据源[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)。  
  
 如果提交失败时在手动模式下，事务将保持活动状态;您可以选择回滚事务，或重试提交操作。 如果提交操作失败时在自动事务模式下，事务将自动回滚;事务不能为非活动状态。  
  
 有关详细信息，请参阅[SQLTransact](../../odbc/reference/syntax/sqltransact-function.md)中*ODBC 程序员参考*。
