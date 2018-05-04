---
title: 实现说明 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7ec14b9c-69b8-4c6e-838a-88d1ebdc8725
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4f707c99b626b27bd35de011e8d1eb78d801e614
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="implementation-notes"></a>实现说明
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本部分介绍如何实现 ODBC 游标库。 它介绍的是光标库维护其缓存、 执行 SQL 语句，以及实现 ODBC 函数。  
  
 本部分包含以下主题。  
  
-   [游标库缓存](../../../odbc/reference/appendixes/cursor-library-cache.md)  
  
-   [处理 SQL 语句](../../../odbc/reference/appendixes/processing-sql-statements.md)  
  
-   [ODBC 函数和游标库](../../../odbc/reference/appendixes/odbc-functions-and-the-cursor-library.md)
