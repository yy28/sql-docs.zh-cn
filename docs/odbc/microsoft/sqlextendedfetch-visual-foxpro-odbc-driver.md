---
title: SQLExtendedFetch （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ecff538198a2b517f980cc63acfc97d29a9f162
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298647"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：级别2  
  
 类似于[SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) ，但使用每个列的数组返回多个行。 如果将游标定义为静态而不是只进，则结果集是可向前滚动的，并且可向后滚动。  
  
 默认情况下，Visual FoxPro ODBC 驱动程序不返回在 FoxPro 表中标记为已删除的行。 标记为删除但尚未从表中删除的行不会包含在结果集游标中。 您可以使用 "[设置已删除](../../odbc/microsoft/set-deleted-command.md)" 命令更改此行为。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) 。
