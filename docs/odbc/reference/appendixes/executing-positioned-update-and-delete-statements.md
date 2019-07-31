---
title: 执行定位更新和删除语句 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2c69f784c2ce7c29cb49c81bf23f34a9cad12089
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913618"
---
# <a name="executing-positioned-update-and-delete-statements"></a>执行定位更新和删除语句
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 应用程序提取的数据块后**SQLFetchScroll**，它可以更新或删除在块中的数据。 若要执行定位的更新或删除，应用程序：  
  
1.  调用**SQLSetPos**将游标定位在要更新或删除的行。  
  
2.  构造定位的 update 或 delete 语句使用以下语法：  
  
     **更新** *表名称*  
  
     **设置** *列标识符* **=** {*表达式* &#124; **NULL**}  
  
     [ **，** *列标识符* **=** {*表达式* &#124; **NULL**}]  
  
     **WHERE CURRENT OF** *游标名称*  
  
     **DELETE FROM** *l e-n* **WHERE CURRENT OF** *游标名称*  
  
     构造的最简单办法**设置**子句中定位的 update 语句是使用参数标记的每个列进行更新，并且使用**SQLBindParameter**要绑定到行集的缓冲区要更新的行。 在这种情况下，该参数的 C 数据类型将作为行集缓冲区的 C 数据类型相同。  
  
3.  如果它将执行定位的 update 语句，更新当前行的行集缓冲区。 已成功执行定位的更新语句之后, 该游标库中的值复制的当前行中的每一列到其缓存。  
  
    > [!CAUTION]  
    >  如果应用程序不会正确更新的行集缓冲区执行定位的更新语句前，缓存中的数据执行语句后将不正确。  
  
4.  执行定位的 update 或 delete 语句使用不同语句比与游标相关联的语句。  
  
    > [!CAUTION]  
    >  **其中**子句通过游标库来标识当前行来构造可能无法识别的任何行，标识不同的行，或标识多个行。 有关详细信息，请参阅[构造搜索语句](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 所有定位 update 和 delete 语句需要一个游标名称。 若要指定游标名称，应用程序调用**SQLSetCursorName**打开游标之前。 若要使用驱动程序生成的游标名称，应用程序调用**SQLGetCursorName**打开游标后。  
  
 光标位置后库执行定位的更新或 delete 语句的状态数组、 行集缓冲区和维护由游标库缓存包含下表中显示的值。  
  
|使用语句|行状态数组中的值|中的值<br /><br /> 行集的缓冲区|中的值<br /><br /> 缓存缓冲区|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|定位的更新|SQL_ROW_UPDATED|新值 [1]|新值 [1]|  
|定位的删除|SQL_ROW_DELETED|旧值|旧值|  
  
 [1] 应用程序必须执行定位的更新语句中; 前更新的行集缓冲区中的值执行定位的更新语句之后，该游标库复制值的行集缓冲区中到其缓存。
