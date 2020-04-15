---
title: SQLTransact（可视化福克斯Pro ODBC驱动程序） |微软文档
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
ms.openlocfilehash: 3910f24578bcbc409a84573e994c0680ed5949b2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299217"
---
# <a name="sqltransact-visual-foxpro-odbc-driver"></a>SQLTransact（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持： 完整  
  
 ODBC API 一致性：核心级别  
  
 请求所有与连接关联的语句句柄 *（hstmt*s） 或与环境句柄关联的所有连接*henv*的所有活动操作的提交或回滚操作。 **SQLTransact**仅适用于[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)的数据源。  
  
 如果在手动模式下提交失败，则事务将保持活动状态;如果提交处于手动模式下，则事务将保持活动状态。您可以选择回滚事务或重试提交操作。 如果在自动事务模式下提交操作失败，则事务将自动回滚;事务不能处于非活动状态。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLTransact。](../../odbc/reference/syntax/sqltransact-function.md)
