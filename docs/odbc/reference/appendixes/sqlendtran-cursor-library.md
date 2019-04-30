---
title: SQLEndTran （游标库） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLEndTran function [ODBC], Cursor Library
ms.assetid: 92340b87-9084-4838-a509-e9ca22d5fd5c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e2e218035473d1ebb980aa5f44da8cc7b8ef843d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199499"
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLEndTran**游标库中的函数。 有关常规信息**SQLEndTran**，请参阅[SQLEndTran 函数](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
 游标库不支持事务，并将传递到调用**SQLEndTran**直接向驱动程序。 但是，该游标库支持游标提交和回滚行为所返回的具有 SQL_CURSOR_ROLLBACK_BEHAVIOR 和 SQL_CURSOR_COMMIT_BEHAVIOR 信息类型的数据源：  
  
-   对于跨事务保留游标的数据源，数据源中回滚的更改将不回滚游标库缓存中。 若要使匹配数据源中的数据缓存，应用程序必须关闭并重新打开游标。  
  
-   关闭游标事务边界的数据源，游标库关闭游标，并删除在连接上的所有语句缓存。  
  
-   对于删除预定义的语句在事务边界的数据源，该应用程序必须 reprepare 继续重新执行它们在连接上的所有预定义的语句。
