---
title: ODBC 静态光标 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b99566c473e88684e8b092a5ac9fc899e7dce177
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282438"
---
# <a name="odbc-static-cursors"></a>ODBC 静态游标
静态游标是结果集显示为静态的游标。 它通常不会检测打开游标后对结果集的成员身份、顺序或值所做的更改。 例如，假设静态游标获取一行，然后另一个应用程序更新该行。 如果静态游标重新提取行，则它看到的值将保持不变，尽管其他应用程序进行了更改。  
  
 静态游标可以检测自己的更新、删除和插入，尽管它们不需要这样做。 特定静态游标是否检测到这些更改将通过**SQLGetInfo**中的SQL_STATIC_SENSITIVITY选项进行报告。 静态游标永远不会检测到其他更新、删除和插入。  
  
 SQL_ATTR_ROW_STATUS_PTR语句属性指定的行状态数组可以包含任何行的SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO或SQL_ROW_ERROR。 它返回SQL_ROW_UPDATED、SQL_ROW_DELETED或SQL_ROW_ADDED，用于游标更新、删除或插入的行，前提是游标可以检测到此类更改。  
  
 静态游标通常是通过锁定结果集中的行或复制结果集或快照实现的。 尽管锁定行相对容易操作，但它有显著减少并发的缺点是显著减少并发性。 制作副本允许更大的并发性，并允许游标通过修改副本来跟踪其自己的更新、删除和插入。 但是，复制的制作成本更高，并且可能会由于其他数据被其他人更改而偏离基础数据。
