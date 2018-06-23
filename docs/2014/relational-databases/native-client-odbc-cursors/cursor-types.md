---
title: 游标类型 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC applications, cursors
- cursors [ODBC], types
- ODBC cursors, types
ms.assetid: 3a916cc7-f352-42cb-8b83-f78e06cef991
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e63cceadf80da13956ea576db50459279a251b51
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029227"
---
# <a name="cursor-types"></a>游标类型
  ODBC 定义受 Microsoft 的四种游标类型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序。 这些游标能力检测到结果集的更改而变化的资源中，它们使用，如内存和空间中**tempdb**。 游标仅当尝试重新提取行时才会检测到对这些行的更改；数据源无法通知游标对当前提取行的更改。 游标检测并非由游标执行的更改的功能也受事务隔离级别的影响。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持以下四种 ODBC 游标类型：  
  
-   只进游标不支持滚动；它们只支持游标按从头到尾的顺序提取行。  
  
-   静态游标内置的**tempdb**时打开的游标。 它们始终显示结果集和打开游标时。 它们从不会反映对数据的更改。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 静态游标始终是只读的。 因为静态服务器游标生成的工作表中为**tempdb**，游标的结果集的大小不能超过允许的最大行大小[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   打开由键集驱动的游标时，该游标的结果集中各行的成员身份和顺序是固定的。 可通过游标显示对非键列的更改。  
  
-   动态游标与静态游标相对。 动态游标反映对结果集中的行的所有更改。 结果集中的行数据值、顺序和成员在每次提取时都会改变。  
  
## <a name="see-also"></a>请参阅  
 [使用游标， &#40;ODBC&#41;](using-cursors-odbc.md)  
  
  