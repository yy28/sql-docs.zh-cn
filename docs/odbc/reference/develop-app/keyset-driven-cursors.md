---
title: 由键集驱动的游标 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: be6dc5a164220befb534368eace4f51f4dbd84e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213448"
---
# <a name="keyset-driven-cursors"></a>由键集驱动的游标
由键集驱动游标静态和动态游标之间在于它能够检测更改。 比如静态游标，它不会始终检测对结果集的成员身份和顺序的更改。 类似动态游标，它检测到的行值发生更改的结果集 （取决于该事务，如 SQL_ATTR_TXN_ISOLATION 连接属性所设置的隔离级别） 中。  
  
 当打开由键集驱动游标时，它将保存整个结果集; 的密钥这修复了明显的成员资格和顺序的结果集。 当游标滚动整个结果集时，它在此使用键*由键集*检索每个行的当前数据值。 例如，假设由键集驱动游标提取行和另一个应用程序，然后更新该行。 如果游标提取此行，发现的值将是新的因为它 refetched 使用它的键的行。 因此，由键集驱动游标始终检测自身和其他用户所做的更改。  
  
 当光标尝试检索已删除的行时，此行显示为一个"hole"中的结果集：行键存在于键集中，但行不再存在于结果集中。 如果更新某一行中的密钥值，则将该行视为已删除和然后插入，因此这样的行也将显示为结果集中的孔。 而由键集驱动游标始终可以检测到删除其他人的行，它可以根据需要删除的密钥的行它本身将从删除由键集。 执行此操作的由键集驱动游标无法检测到自己的删除。 特定的由键集驱动游标是否检测到其自身删除通过中的 SQL_STATIC_SENSITIVITY 选项将报告**SQLGetInfo**。  
  
 由其他人插入的行是永远不会对由键集驱动游标可见，因为这些行没有键存在于由键集。 但是，由键集驱动游标可以根据需要添加项的行它将自身插入到由键集。 执行此操作的由键集驱动游标可以检测到其自己插入。 特定的由键集驱动游标是否检测到其自己插入通过中的 SQL_STATIC_SENSITIVITY 选项将报告**SQLGetInfo**。  
  
 将 SQL_ATTR_ROW_STATUS_PTR 语句属性指定的行状态数组可以包含 SQL_ROW_SUCCESS、 SQL_ROW_SUCCESS_WITH_INFO 或 SQL_ROW_ERROR 对于任何行。 它将返回 SQL_ROW_UPDATED、 SQL_ROW_DELETED 或作为更新后，检测到的行的 SQL_ROW_ADDED 删除，或插入。  
  
 由键集驱动的游标通常是通过创建一个包含结果集中的每个行的键的临时表实现的。 游标还必须确定是否已更新行，因为此表通常还包含具有行版本控制信息的列。  
  
 若要滚动对原始结果集，由键集驱动游标的临时表上打开静态游标。 若要检索原始结果集的行中，将光标首次从临时表中检索相应的密钥，然后检索行的当前值。 如果使用块游标，游标必须检索多个键和行。
