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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d58d7885eed1a8ed0611470f29cb24e8072afcb9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053799"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：级别2  
  
 类似于[SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) ，但使用每个列的数组返回多个行。 如果将游标定义为静态而不是只进，则结果集是可向前滚动的，并且可向后滚动。  
  
 默认情况下，Visual FoxPro ODBC 驱动程序不返回在 FoxPro 表中标记为已删除的行。 标记为删除但尚未从表中删除的行不会包含在结果集游标中。 您可以使用 "[设置已删除](../../odbc/microsoft/set-deleted-command.md)" 命令更改此行为。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md) 。
