---
title: "混合游标 |Microsoft 文档"
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
- mixed cursors [ODBC]
- cursors [ODBC], dynamic
- keyset-driven cursors [ODBC]
- dynamic cursors [ODBC]
- cursors [ODBC], key-set driven
- cursors [ODBC], mixed
ms.assetid: 9beb2db9-0b6d-491d-9529-d64e64e59014
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 16369d96931bd2b01d644756ab7e1e22fd325a85
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="mixed-cursors"></a>混合的游标
混合的光标位于键集驱动游标和动态游标的组合。 如果结果集太大而无法规范的合理保存整个结果集的密钥，则会使用它。 混合的游标实现通过创建小于整个结果集，但大于行集中键集。  
  
 只要应用程序滚动在键集内，则行为将是键集驱动。 如果应用程序滚动外键集时，则行为是动态： 提取请求的行并创建新的键集游标。 创建新密钥集后，该行为将恢复为键集驱动内该键集。  
  
 例如，假设一个结果集具有 1,000 行，并具有键集大小 100 和行集大小的 10 使用混合的光标。 当第一个行集提取时，光标将创建键集包含的前 100 行的键。 然后，它返回前 10 行，根据请求。  
  
 现在，假设另一个应用程序删除行 11 和 101。 如果光标尝试检索第 11 行，它将遇到一个口，因为它具有此行的键，但没有行存在;这是键集驱动的行为。 如果光标尝试检索第 101，光标将检测不到行是缺少，因为它不具有行的键。 相反，它将检索先前行 102。 这是动态游标行为。  
  
 混合的光标相当于键集驱动游标时的键集大小等同于结果集大小。 混合的光标相当于动态游标键集大小等于 1 时。

