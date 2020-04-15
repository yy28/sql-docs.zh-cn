---
title: SQL 扩展获取（可视化福克斯 Pro ODBC 驱动程序） |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298647"
---
# <a name="sqlextendedfetch-visual-foxpro-odbc-driver"></a>SQLExtendedFetch（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持： 完整  
  
 ODBC API 符合性：2 级  
  
 与[SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md)类似，但使用每个列的数组返回多行。 结果集是可向前滚动的，如果游标定义为静态的，而不是仅向前滚动，则可以向后滚动。  
  
 默认情况下，Visual FoxPro ODBC 驱动程序不会返回在 FoxPro 表中标记为已删除的行。 标记为删除但尚未从表中删除的行不包括在结果集游标中。 您可以使用[SET DELETED](../../odbc/microsoft/set-deleted-command.md)命令更改此行为。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQL 扩展获取](../../odbc/reference/syntax/sqlextendedfetch-function.md)。
