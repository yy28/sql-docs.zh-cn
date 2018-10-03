---
title: 游标类型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, cursors
- ODBC applications, cursors
- cursors [ODBC], types
- ODBC cursors, types
ms.assetid: 3a916cc7-f352-42cb-8b83-f78e06cef991
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d88b48c1fc4166b32821da9cdaaa5eb7f6c2e60
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072287"
---
# <a name="cursor-types"></a>游标类型
  ODBC 定义四种游标类型，Microsoft 支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序。 这些游标检测结果集变化的能力会有所不同并且的资源中使用，如内存和空间中**tempdb**。 游标仅当尝试重新提取行时才会检测到对这些行的更改；数据源无法通知游标对当前提取行的更改。 游标检测并非由游标执行的更改的功能也受事务隔离级别的影响。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持以下四种 ODBC 游标类型：  
  
-   只进游标不支持滚动；它们只支持游标按从头到尾的顺序提取行。  
  
-   静态游标内置的**tempdb**打开游标时。 它们始终显示结果集打开游标时一样。 它们从不会反映对数据的更改。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 静态游标始终是只读的。 由于对静态服务器游标生成的工作表中作为**tempdb**，游标结果集的大小不能超过允许的最大行大小[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
-   打开由键集驱动的游标时，该游标的结果集中各行的成员身份和顺序是固定的。 可通过游标显示对非键列的更改。  
  
-   动态游标与静态游标相对。 动态游标反映对结果集中的行的所有更改。 结果集中的行数据值、顺序和成员在每次提取时都会改变。  
  
## <a name="see-also"></a>请参阅  
 [使用游标&#40;ODBC&#41;](using-cursors-odbc.md)  
  
  
