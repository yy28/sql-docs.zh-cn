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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a91dacf8ea9c0ed0db2c3b64634ddd53b854a534
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307432"
---
# <a name="mixed-cursors"></a>混合游标

混合游标是由键集驱动的游标和动态游标的组合。 如果结果集太大而无法合理保存整个结果集的密钥，则可以使用此方法。 混合游标是通过创建一个小于整个结果集但大于行集的键集来实现的。  
  
 只要应用程序在键集中滚动，行为就是由键集驱动的。 当应用程序在键集外滚动时，行为是动态的：游标提取请求的行并创建新的键集。 创建新的键集后，该行为会恢复为该键集中的键集驱动程序。  
  
 例如，假设有一个结果集包含1000行，并使用键集大小为100且行集大小为10的混合游标。 提取第一个行集时，游标将创建由前100行的键组成的键集。 然后，它会根据请求返回前10行。  
  
 现在，假设另一个应用程序删除第11行和第101行。 如果游标尝试检索第11行，它会遇到间隔，因为它具有此行的键，但不存在任何行;这是由键集驱动的行为。 如果游标尝试检索行101，则游标将不会检测到行是否缺失，因为它没有行的键。 相反，它将检索第102行。 这是动态游标行为。  
  
 当键集大小等于结果集大小时，混合游标等效于由键集驱动的游标。 当键集大小等于1时，混合游标等效于动态游标。
