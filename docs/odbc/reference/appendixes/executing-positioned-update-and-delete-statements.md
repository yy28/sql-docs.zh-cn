---
title: 执行定位更新和删除语句 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- ODBC cursor library [ODBC], positioned update or delete
ms.assetid: 1d64f309-2a6e-4ad1-a6b5-e81145549c56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96a1aa891ef8ba26c6c239cf35e62a8f36018e65
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306998"
---
# <a name="executing-positioned-update-and-delete-statements"></a>执行定位更新和删除语句
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 应用程序使用**SQLFetchScroll**获取数据块后，可以更新或删除块中的数据。 要执行定位的更新或删除，应用程序：  
  
1.  调用**SQLSetPos**将光标放置在要更新或删除的行上。  
  
2.  使用以下语法构造定位的更新或删除语句：  
  
     **更新***表名称*  
  
     **设置***列标识符***=**= &#124; **NULL**的*表达式*|  
  
     [**，***列标识符***=**]*表达式*&#124; **NULL**]  
  
     **其中***光标名称的*当前  
  
     **从***表名中删除**游标名称***的当前**位置  
  
     在定位更新语句中构造**SET**子句的最简单方法是对要更新的每个列使用参数标记，并使用**SQLBind 参数**将这些参数绑定到要更新行的行集缓冲区。 在这种情况下，参数的 C 数据类型将与行集缓冲区的 C 数据类型相同。  
  
3.  如果当前行将执行定位的更新语句，则更新当前行的行集缓冲区。 成功执行定位的更新语句后，游标库将当前行中每列的值复制到其缓存。  
  
    > [!CAUTION]  
    >  如果应用程序在执行定位的更新语句之前未正确更新行集缓冲区，则在执行语句后，缓存中的数据将不正确。  
  
4.  使用与游标关联的语句不同的语句执行定位的更新或删除语句。  
  
    > [!CAUTION]  
    >  游标库为标识当前行而构造的**WHERE**子句可能无法标识任何行、标识其他行或标识多行。 有关详细信息，请参阅[构造搜索语句](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 所有定位的更新和删除语句都需要游标名称。 要指定游标名称，应用程序在打开游标之前调用**SQLSetCursorName。** 要使用驱动程序生成的游标名称，应用程序在打开游标后调用**SQLGetCursorName。**  
  
 游标库执行定位的更新或删除语句后，游标库维护的状态数组、行集缓冲区和缓存包含下表中显示的值。  
  
|使用语句|行状态数组中的值|中的值<br /><br /> 排集缓冲区|中的值<br /><br /> 缓存缓冲区|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|定位更新|SQL_ROW_UPDATED|新值[1]|新值[1]|  
|定位删除|SQL_ROW_DELETED|旧值|旧值|  
  
 [1] 应用程序在执行定位的更新语句之前必须更新行集缓冲区中的值;执行定位的更新语句后，游标库将行集缓冲区中的值复制到其缓存。
