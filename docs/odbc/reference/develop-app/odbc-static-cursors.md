---
title: 功能，ODBC 静态游标 |Microsoft 文档
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
helpviewer_keywords:
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c2e6835d818d1e1d5aba7b54497f4a95f0bc150
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-static-cursors"></a>功能，ODBC 静态游标
静态游标是一个结果集似乎是静态的。 它通常不检测在对成员资格、 顺序或值的结果集打开光标后所做的更改。 例如，假定静态游标提取行和另一个应用程序，然后更新该行。 静态游标提取此行，如果它发现的值是不变，尽管已被其他应用程序所做的更改。  
  
 静态游标可以检测其自己的更新、 删除和插入，虽然不需要它们来执行此操作。 通过中的 SQL_STATIC_SENSITIVITY 选项报告特定静态游标是否检测这些更改的是**SQLGetInfo**。 静态游标永远不会检测其他更新、 删除和插入。  
  
 SQL_ATTR_ROW_STATUS_PTR 语句属性指定行状态数组可以包含 SQL_ROW_SUCCESS、 SQL_ROW_SUCCESS_WITH_INFO 或 SQL_ROW_ERROR 任何行。 对于，它返回 SQL_ROW_UPDATED、 SQL_ROW_DELETED 或 SQL_ROW_ADDED 更新、 删除或插入的光标，假设光标可以检测此类更改的行。  
  
 静态游标是通常实现通过锁定结果集中的行或使副本，或快照，结果的设置。 尽管锁定的行是相对较为容易，但它具有显著减少并发的缺点。 制作的副本允许更大的并发和允许光标能够跟踪其自己的更新、 删除和插入的对副本进行修改。 但是，副本是开销更大到进行数据更改其他人可以从基础数据发生偏离。
