---
title: "键集驱动游标 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- keyset-driven cursors [ODBC]
- cursors [ODBC], key-set driven
ms.assetid: 01769f43-1d9c-4685-84fa-15a6465335e9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7cbd7ca159b09ee1482139ef76bfff48115a62bd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="keyset-driven-cursors"></a>键集驱动游标
键集驱动游标静态和动态游标之间在于它能够检测更改。 如静态游标，它不始终检测到的成员资格和顺序的结果集的更改。 动态游标，像它未在结果集中 （遵从事务，如所 SQL_ATTR_TXN_ISOLATION 连接属性设置的隔离级别） 检测更改的行的值。  
  
 当打开键集驱动游标时，它将保存整个结果集; 的密钥这会修复的明显的成员资格和顺序的结果集。 当光标滚动整个结果集时，它使用在此密钥*键集*检索每个行的当前数据值。 例如，假设键集驱动游标提取行和另一个应用程序，然后更新该行。 如果此行光标，它发现的值将是新的因为它 refetched 使用其密钥的行。 因此，键集驱动游标始终检测到其自身和其他用户所做的更改。  
  
 当光标尝试检索已被删除的行时，该行将显示为的结果集的"漏洞": 行的键存在于键集，但结果集中不存在的行。 如果一行中的密钥值更新时，行被视为已删除，然后插入，因此这样的行也显示为结果集中漏洞。 虽然键集驱动游标总是能够检测到被其他人删除的行，它可以根据需要删除键行它本身从删除键集。 执行此操作的键集驱动游标无法检测到自己的删除。 特定的键集驱动游标是否检测到其自身删除通过中的 SQL_STATIC_SENSITIVITY 选项报告**SQLGetInfo**。  
  
 由其他插入的行是永远不会对键集驱动游标可见，因为这些行没有键存在于键集。 但是，键集驱动游标可以选择添加密钥为行它将自身插入到键集。 执行此操作的键集驱动游标可以检测到其自己的插入。 特定的键集驱动游标是否检测到其自己插入通过中的 SQL_STATIC_SENSITIVITY 选项报告**SQLGetInfo**。  
  
 SQL_ATTR_ROW_STATUS_PTR 语句属性指定行状态数组可以包含 SQL_ROW_SUCCESS、 SQL_ROW_SUCCESS_WITH_INFO 或 SQL_ROW_ERROR 任何行。 它将返回 SQL_ROW_UPDATED、 SQL_ROW_DELETED 或作为更新，检测到的行的 SQL_ROW_ADDED 删除，或者插入。  
  
 键集驱动游标通常通过创建一个包含结果集中的每一行的键的临时表实现。 因为光标还必须确定此表是否已更新行时，通常还包含具有行版本控制信息的列。  
  
 若要通过原始结果集滚动，键集驱动游标，请打开的临时表上的静态游标。 若要检索原始结果集中的行，光标首先从临时表中检索相应的密钥，然后检索行的当前值。 如果使用块游标，光标必须检索多个键和行。
