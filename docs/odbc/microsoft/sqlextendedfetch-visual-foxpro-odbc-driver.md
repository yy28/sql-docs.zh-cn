---
title: "SQLExtendedFetch （Visual FoxPro ODBC 驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLExtendedFetch function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b28af112-fb47-4143-b11e-3b743b2ae1b8
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ece0e07d4da4c19845100e465338d97810d14162
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch （Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序相关的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 完整  
  
 ODBC API 一致性： 级别 2  
  
 类似于[SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md)但返回为每一列使用数组的多个行。 结果集是可向前滚动，并可向后滚动如果定义为静态、 不只进游标。  
  
 默认情况下，Visual FoxPro ODBC 驱动程序不返回标记为 FoxPro 表中已删除的行。 在结果集游标不包括标记为删除但尚未从表中删除的行。 你可以通过更改此行为[设置删除](../../odbc/microsoft/set-deleted-command.md)命令。  
  
 有关详细信息，请参阅[SQLExtendedFetch](../../odbc/reference/syntax/sqlextendedfetch-function.md)中*ODBC 程序员参考*。
