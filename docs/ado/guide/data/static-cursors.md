---
title: 静态游标 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], static
- static cursors [ADO]
ms.assetid: cce93ace-c4ed-4c6c-940c-28a50ff2fd12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e8815522ee4f9a4221887696a23a201910d7cfad
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654185"
---
# <a name="static-cursors"></a>静态游标
静态游标始终会显示结果集与第一次打开游标时一样。 具体取决于实现，静态游标是只读或读/写，并提供向前和向后滚动。 静态游标通常不会检测到的成员身份、 顺序或值的结果集打开游标后所做的更改。 静态游标可能检测其自己的更新、 删除和插入，尽管不需要它们来执行此操作。  
  
 静态游标永远不会检测其他更新、 删除和插入。 例如，假定静态游标提取行和另一个应用程序，然后更新该行。 如果应用程序提取此行从静态游标，它看到的值保持不变，尽管其他应用程序所做的更改。 支持所有类型的滚动，但提供程序可能会或可能不支持书签。  
  
 如果你的应用程序并不需要检测数据更改，并需要滚动，静态游标是最佳选择。 使用**adOpenStatic CursorTypeEnum**以指示你想要使用静态游标在 ADO 中。  
  
## <a name="see-also"></a>请参阅  
 [只进游标](../../../ado/guide/data/forward-only-cursors.md)   
 [由键集游标](../../../ado/guide/data/keyset-cursors.md)   
 [动态游标](../../../ado/guide/data/dynamic-cursors.md)
