---
title: "Update 和 Delete 语句执行定位 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positioned deletes [ODBC]
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- ODBC cursor library [ODBC], positioned update or delete
ms.assetid: 1d64f309-2a6e-4ad1-a6b5-e81145549c56
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 78bdb77c8aa4d9351e040b97d9690bb09374856d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="executing-positioned-update-and-delete-statements"></a>正在执行的定位的 Update 和 Delete 语句
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 应用程序提取的数据块后**SQLFetchScroll**，它能够更新或删除块中的数据。 若要执行的定位的更新或删除、 应用程序：  
  
1.  调用**SQLSetPos**将光标定位在要更新或删除的行上。  
  
2.  构造定位的 update 或 delete 语句具有以下语法：  
  
     **更新***表名称*  
  
     **设置***列标识符*  **=**  {*表达式*&#124;**NULL**}  
  
     [**，** *列标识符*  **=**  {*表达式*&#124;**NULL**}]  
  
     **WHERE CURRENT OF** *游标名称*  
  
     **DELETE FROM** *表名* **WHERE CURRENT OF** *游标名称*  
  
     构造的最简单办法**设置**中定位的 update 语句子句是使用为每个列的参数标记来更新，并且使用**SQLBindParameter**要绑定到的行集缓冲区要更新的行。 在这种情况下，该参数的 C 数据类型将作为行集缓冲区的 C 数据类型相同。  
  
3.  如果它会执行的定位的更新语句会更新当前行的行集缓冲区。 成功执行的定位的更新语句之后, 的光标库将的值复制从当前行中每一列到其缓存。  
  
    > [!CAUTION]  
    >  如果应用程序不会正确更新的行集缓冲区执行的定位的更新语句之前，缓存中的数据会不正确之后执行的语句。  
  
4.  执行的定位的更新或 delete 语句使用比与游标关联的语句的不同语句。  
  
    > [!CAUTION]  
    >  **其中**子句通过游标库来标识当前行构造可能无法识别的任何行，标识不同的行，或标识多个行。 有关详细信息，请参阅[构造搜索语句](../../../odbc/reference/appendixes/constructing-searched-statements.md)。  
  
 所有定位 update 和 delete 语句需要游标名称。 若要指定游标名称，应用程序调用**SQLSetCursorName**打开光标之前。 若要使用该驱动程序由生成的游标名，应用程序调用**SQLGetCursorName**光标在打开后。  
  
 光标位置后库执行的定位的更新或 delete 语句、 状态数组、 行集缓冲区和维护的是光标库的缓存包含下表中显示的值。  
  
|使用语句|行状态数组中的值|中的值<br /><br /> 行集缓冲区|中的值<br /><br /> 缓存缓冲区|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|定位的更新|SQL_ROW_UPDATED|新值 [1]|新值 [1]|  
|定位的删除|SQL_ROW_DELETED|旧值|旧值|  
  
 [1] 应用程序必须在执行定位的更新语句中; 前更新的行集缓冲区中的值在执行的定位的 update 语句之后, 的是光标库将的值复制行集缓冲区中到其缓存。

