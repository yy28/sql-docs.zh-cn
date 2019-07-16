---
title: 混合游标 |Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mixed cursors [ODBC]
- cursors [ODBC], dynamic
- keyset-driven cursors [ODBC]
- dynamic cursors [ODBC]
- cursors [ODBC], key-set driven
- cursors [ODBC], mixed
ms.assetid: 9beb2db9-0b6d-491d-9529-d64e64e59014
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97da67bca185cd86de944e8bccc86d2b4c149b0d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086375"
---
# <a name="mixed-cursors"></a>混合游标

混合的游标是由键集驱动游标和动态游标的组合。 使用时的结果集太大而无法合理地保存整个结果集的密钥。 混合的游标实现通过创建小于整个结果集，但大于行集由键集。  
  
 只要应用程序滚动内由键集时，行为是由键集驱动。 如果外键集滚动应用程序，则行为是动态：游标提取请求的行，并创建新的由键集。 创建新的由键集后，行为将恢复为由键集驱动的键集内。  
  
 例如，假设结果集包含 1,000 行，并使用混合的游标键集大小为 100、 行集大小为 10。 时提取第一个行集，游标将创建由键集包含的前 100 行的键。 然后根据请求返回前 10 行。  
  
 现在假设另一个应用程序删除行 11 和 101。 如果光标尝试检索第 11 行，因为它有该行的键，但没有行存在，则，它将会遇到间隔这是由键集驱动的行为。 如果尝试检索第 101 游标，游标将不会检测行缺少，因为它不具有行的键。 相反，它会检索先前行 102。 这是动态游标行为。  
  
 混合的游标相当于由键集驱动游标时由键集大小等于的结果集大小。 混合的游标相当于动态游标键集大小为 1 时。
