---
title: 键集驱动光标 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- keyset-driven cursors [ODBC]
- cursors [ODBC], key-set driven
ms.assetid: 01769f43-1d9c-4685-84fa-15a6465335e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 814fca7d48f50aab51b6b4f7e34835be8c412e9c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306202"
---
# <a name="keyset-driven-cursors"></a>由键集驱动的游标
键集驱动的游标位于静态游标和动态游标之间，用于检测更改。 比如静态游标，它不会始终检测对结果集的成员身份和顺序的更改。 与动态游标一样，它确实检测结果集中行值的更改（受事务的隔离级别的约束，由SQL_ATTR_TXN_ISOLATION连接属性设置）。  
  
 打开键集驱动的游标时，它会保存整个结果集的键;这将修复结果集的明显成员身份和顺序。 当游标滚动到结果集时，它使用此*键集中*的键检索每行的当前数据值。 例如，假设键集驱动的游标获取一行，然后另一个应用程序更新该行。 如果光标重新提取行，则它看到的值是新的值，因为它使用其键重新提取行。 因此，键集驱动的游标始终检测自己和其他人所做的更改。  
  
 当游标尝试检索已删除的行时，此行在结果集中显示为"孔"：该行的键存在于键集中，但该行不再存在于结果集中。 如果更新了行中的键值，则该行将被视为已删除并插入，因此此类行也会在结果集中显示为孔。 虽然键集驱动的游标始终可以检测其他人删除的行，但它可以选择从密钥集中删除自己删除的行的键。 执行此操作的键集驱动游标无法检测到它们自己的删除。 特定键集驱动的游标是否检测到其自己的删除是通过**SQLGetInfo**中的SQL_STATIC_SENSITIVITY选项报告的。  
  
 其他人插入的行永远不会对键集驱动的游标可见，因为键集中中不存在这些行的键。 但是，键集驱动的游标可以选择将其插入自己的行的键添加到键集中。 执行此操作的键集驱动游标可以检测自己的插入。 特定键集驱动的游标是否检测到其自己的插入是通过**SQLGetInfo**中的SQL_STATIC_SENSITIVITY选项报告的。  
  
 SQL_ATTR_ROW_STATUS_PTR语句属性指定的行状态数组可以包含任何行的SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO或SQL_ROW_ERROR。 它返回SQL_ROW_UPDATED、SQL_ROW_DELETED或SQL_ROW_ADDED，用于它检测到的更新、删除或插入的行。  
  
 键集驱动的游标通常是通过创建一个临时表实现的，该表包含结果集中每行的键。 由于游标还必须确定行是否已更新，因此此表通常还包含包含行版本控制信息的列。  
  
 要滚动原始结果集，键集驱动的游标将在临时表上打开静态游标。 若要检索原始结果集中的行，光标首先从临时表中检索相应的键，然后检索该行的当前值。 如果使用块游标，光标必须检索多个键和行。
