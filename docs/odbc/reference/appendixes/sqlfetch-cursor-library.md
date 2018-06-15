---
title: SQLFetch （光标库） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], Cursor Library
ms.assetid: 35a0d493-778b-4fb1-84ee-a13540e2fe0e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 867a541b5135b0577e4e23c83ad18c603227270d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32907482"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch （光标库）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLFetch**光标库中的函数。 有关常规信息**SQLFetch**，请参阅[SQLFetch 函数](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
 当使用的是光标库时，调用**SQLFetch**不能与调用混合**SQLFetchScroll**或**SQLExtendedFetch**。  
  
 如果**SQLFetch**称为 SQL_ATTR_ROW_ARRAY_SIZE 设置为值大于 1，与游标库将传递到该驱动程序的调用。 如果该驱动程序是 ODBC 2。*x*驱动程序，将忽略的行集大小和对**SQLFetch**将返回一行数据。  
  
 如果与 ODBC 2 一起使用的是光标库。*x*驱动程序，偏移量 （按定义 SQL_ATTR_ROW_BIND_OFFSET_PTR 语句属性） 的绑定不使用时**SQLFetch**调用。  
  
 应用程序加载的是光标库后，不能调用**SQLFetch**提取书签列。 游标库将传递到调用**SQLFetch**通过为该驱动程序，但该函数调用，启用书签和绑定书签列都会被截获由游标库。
