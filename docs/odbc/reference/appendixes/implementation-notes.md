---
title: 实现说明 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7ec14b9c-69b8-4c6e-838a-88d1ebdc8725
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 95b60ba35a867135cfc1f823e08b1a99f0262ca9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135735"
---
# <a name="implementation-notes"></a>实现说明
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本部分介绍如何实现 ODBC 游标库。 它介绍了游标库如何维护其缓存、执行 SQL 语句并实现 ODBC 函数。  
  
 本部分包含下列主题。  
  
-   [游标库缓存](../../../odbc/reference/appendixes/cursor-library-cache.md)  
  
-   [处理 SQL 语句](../../../odbc/reference/appendixes/processing-sql-statements.md)  
  
-   [ODBC 函数和游标库](../../../odbc/reference/appendixes/odbc-functions-and-the-cursor-library.md)
