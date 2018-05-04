---
title: 键集游标 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Keyset cursors [ADO]
- cursors [ADO], Keyset
ms.assetid: 14b51b17-6fd9-4146-af45-ca4b0fe6d48a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6abebe52390c8c3423cd3c41f212236e051e1972
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="keyset-cursors"></a>键集游标
键集游标提供的功能，以检测更改的静态和动态游标之间的功能。 如静态游标，它不始终检测到的成员资格和顺序的结果集的更改。 动态游标，像它未在结果集中检测更改的行的值。  
  
 键集驱动游标由一组称为键集的唯一标识符 （键） 控制。 键是根据以唯一方式标识结果集中各行的一组列生成的。 键集是从返回的查询语句的所有行的键值的组。  
  
 使用键集驱动游标时，密钥生成和保存游标中每一行，并存储在客户端工作站或服务器上。 访问每个行时，存储的密钥用于从数据源提取当前数据值。 在由键集驱动游标，结果集成员身份被冻结完全填充键集时。 此后，添加件或会影响成员身份的更新不属于的结果集之前重新打开。  
  
 对 （使其通过键集所有者或其他进程） 的数据值的更改是可见的当用户滚动整个结果集。 只有在关闭并重新打开游标，（通过其他进程） 游标外部所做的插入才可见。 从游标内部进行的插入是结果集末尾可见。  
  
 如果键集驱动游标试图来检索已被删除的行，该行将显示为的结果集的"漏洞"。 行的键存在于键集，但结果集中不存在的行。 如果一行中的密钥值更新时，行被视为已删除，然后插入，因此这样的行也显示为结果集中漏洞。 虽然键集驱动游标总是能够检测到其他进程中删除的行，它可以根据需要删除它自己删除的行的键。 执行此操作的键集驱动游标无法检测到自己的删除，因为已经删除了证据。  
  
 对键列的更新操作类似于删除旧密钥跟插入的新密钥。 新的密钥值不可见，如果不通过游标进行更新。 如果通过游标进行更新，新密钥值将会出现在结果集的末尾。  
  
 没有一个变体称为键集驱动标准游标键集驱动游标。 键集驱动的标准游标，在结果集中的行的成员身份和各行的顺序固定的游标打开时，但对值通过游标所有者所做的更改和其他进程提交的更改都可见。 如果更改使某行丧失成员身份或会影响了该行的顺序，行不消失或移动除非关闭并重新打开光标。 插入的数据未显示，但读取行时显示对现有数据的更改。  
  
 键集驱动游标很难正确使用因为向数据更改的敏感度取决于很多不同情况下，按上文所述。 但是，如果你的应用程序不关心并发更新，可以以编程方式处理错误的密钥，并必须直接访问某些键的行键集驱动游标可能适用于你。 使用**adOpenKeyset CursorTypeEnum**以指示你想要使用 ADO 中的键集游标。  
  
## <a name="see-also"></a>另请参阅  
 [只进游标](../../../ado/guide/data/forward-only-cursors.md)   
 [静态游标](../../../ado/guide/data/static-cursors.md)   
 [动态游标](../../../ado/guide/data/dynamic-cursors.md)
