---
title: 键集驱动游标 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c40fe8c823115c3131a1719185bce8f1506df81
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138844"
---
# <a name="keyset-driven-cursors"></a>由键集驱动的游标
由键集驱动的游标在其检测更改的能力中是静态游标和动态游标。 比如静态游标，它不会始终检测对结果集的成员身份和顺序的更改。 与动态游标类似，它确实检测到结果集中的行值更改（根据 SQL_ATTR_TXN_ISOLATION 连接属性设置的事务的隔离级别）。  
  
 当打开由键集驱动的游标时，它会保存整个结果集的键;这会修复结果集的外观成员身份和顺序。 当光标滚动到结果集时，它将使用此*键*集中的键来检索每行的当前数据值。 例如，假设由键集驱动的游标提取行，另一个应用程序然后更新该行。 如果游标 refetches 行，则它看到的值是新的值，因为它使用它的键对行进行制约。 因此，由键集驱动的游标始终检测自身和其他人所做的更改。  
  
 当游标尝试检索已删除的行时，该行将在结果集中显示为 "洞"：行的键存在于键集中，但是行在结果集中不再存在。 如果更新了行中的键值，则会将该行视为已被删除然后插入，因此此类行还会在结果集中显示为洞。 尽管由键集驱动的游标始终可以检测其他人删除的行，但可以选择删除它从键集中删除的行的键。 执行此操作的由键集驱动的游标无法检测自己的删除。 特定的由键集驱动的游标是否检测到其自己的删除通过**SQLGetInfo**中的 SQL_STATIC_SENSITIVITY 选项报告。  
  
 其他人插入的行永远不会对由键集驱动的游标可见，因为在键集中没有这些行的键。 但是，由键集驱动的游标可以选择为它将自身插入到键集的行添加键。 执行此操作的由键集驱动的游标可以检测自己的插入。 特定的由键集驱动的游标是否检测到其自己的插入通过**SQLGetInfo**中的 SQL_STATIC_SENSITIVITY 选项报告。  
  
 SQL_ATTR_ROW_STATUS_PTR 语句特性指定的行状态数组可以包含任意行的 SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO 或 SQL_ROW_ERROR。 它将为它检测到更新、删除或插入的行返回 SQL_ROW_UPDATED、SQL_ROW_DELETED 或 SQL_ROW_ADDED。  
  
 通常通过创建一个临时表来实现键集驱动游标，其中包含结果集中每一行的键。 由于游标还必须确定是否已更新行，因此此表通常还包含具有行版本控制信息的列。  
  
 若要在原始结果集上方滚动，由键集驱动的游标会在临时表上打开一个静态游标。 若要在原始结果集中检索行，游标首先从临时表中检索相应的键，然后检索该行的当前值。 如果使用块游标，则游标必须检索多个键和行。
