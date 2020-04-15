---
title: 混合光标 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307432"
---
# <a name="mixed-cursors"></a>混合游标

混合游标是键集驱动的游标和动态游标的组合。 当结果集太大而无法合理地保存整个结果集的键时，将使用它。 通过创建小于整个结果集但大于行集的键集实现混合游标。  
  
 只要应用程序在密钥集中滚动，该行为就是按键集驱动的。 当应用程序在密钥集外部滚动时，行为是动态的：游标获取请求的行并创建新的键集。 创建新键集后，该行为将恢复为该键集中内的键集驱动。  
  
 例如，假设结果集具有 1，000 行，并使用键集大小为 100 和行集大小为 10 的混合游标。 提取第一个行集时，光标将创建一个键集，其中包含前 100 行的键。 然后，它根据需要返回前 10 行。  
  
 现在假设另一个应用程序删除行 11 和 101。 如果游标尝试检索行 11，它将遇到间隙，因为它具有此行的键，但不存在任何行;这是键集驱动的行为。 如果游标尝试检索行 101，光标将不会检测到该行丢失，因为它没有该行的键。 相反，它将检索以前第 102 行的内容。 这是动态游标行为。  
  
 当键集大小等于结果集大小时，混合游标等效于键集驱动的游标。 当键集大小等于 1 时，混合游标等效于动态游标。
