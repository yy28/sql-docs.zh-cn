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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053799"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持：完全  
  
 ODBC API 一致性：级别 2  
  
 类似于[SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md)但返回的每个列使用数组的多个行。 结果集是可向前滚动，并可向后滚动如果定义为静态，不只进游标。  
  
 默认情况下，Visual FoxPro ODBC 驱动程序不返回标记为 FoxPro 表中已删除的行。 在结果集游标不包括标记为删除但尚未从表中删除的行。 可以通过更改此行为[设置删除](../../odbc/microsoft/set-deleted-command.md)命令。  
  
 有关详细信息，请参阅[SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md)中*ODBC 程序员参考*。
