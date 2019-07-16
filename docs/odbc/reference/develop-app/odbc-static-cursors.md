---
title: ODBC 静态游标 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bcb7c39d39492b91c0b62c5eff2229eb5f61df6b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987834"
---
# <a name="odbc-static-cursors"></a>ODBC 静态游标
静态游标是一个结果集似乎是静态的。 它通常不检测到的成员身份、 顺序或值的结果集打开游标后所做的更改。 例如，假定静态游标提取行和另一个应用程序，然后更新该行。 静态游标提取此行，如果它发现的值保持不变，尽管其他应用程序所做的更改。  
  
 静态游标可以检测其自己的更新、 删除和插入，尽管不需要它们来执行此操作。 特定的静态游标是否检测到这些更改通过中的 SQL_STATIC_SENSITIVITY 选项将报告**SQLGetInfo**。 静态游标永远不会检测其他更新、 删除和插入。  
  
 将 SQL_ATTR_ROW_STATUS_PTR 语句属性指定的行状态数组可以包含 SQL_ROW_SUCCESS、 SQL_ROW_SUCCESS_WITH_INFO 或 SQL_ROW_ERROR 对于任何行。 它返回 SQL_ROW_UPDATED、 SQL_ROW_DELETED 或 SQL_ROW_ADDED 更新或删除，或插入的游标，假定该游标可以检测此类更改的行。  
  
 通常实现通过锁定结果集中的行或使一个副本，或设置结果的快照，静态游标。 尽管锁定行是相对容易地完成，但它具有显著减少可以并发运行的缺点。 制作副本允许更大的并发和允许游标来跟踪其自己的更新、 删除和插入由该副本进行修改。 但是，副本是更多的成本进行并为该数据已更改由其他人可以从基础数据发生偏离。
