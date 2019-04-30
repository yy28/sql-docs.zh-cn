---
title: SQLFetch （游标库） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], Cursor Library
ms.assetid: 35a0d493-778b-4fb1-84ee-a13540e2fe0e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 487a6b357d21ee675fa9594d32c7a2bb7c66e400
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199486"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLFetch**游标库中的函数。 有关常规信息**SQLFetch**，请参阅[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
 当使用游标库时，调用**SQLFetch**不能在其中调用**SQLFetchScroll**或**SQLExtendedFetch**。  
  
 如果**SQLFetch**称为 SQL_ATTR_ROW_ARRAY_SIZE 设置为值大于 1，该游标库将传递给驱动程序的调用。 如果该驱动程序是 ODBC 2。*x*驱动程序，将忽略行集大小和对调用**SQLFetch**将返回一行数据。  
  
 如果游标库与 ODBC 2 一起使用。*x*驱动程序，绑定偏移 （根据 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性的定义） 不可用时**SQLFetch**调用。  
  
 应用程序加载游标库时，不能调用**SQLFetch**来提取书签列。 游标库将传递到调用**SQLFetch**通过驱动程序，但该函数调用，启用书签和绑定的书签列都会被截获由游标库。
