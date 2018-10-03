---
title: 由键集游标 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Keyset cursors [ADO]
- cursors [ADO], Keyset
ms.assetid: 14b51b17-6fd9-4146-af45-ca4b0fe6d48a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2ff246d01254ceb2b526b5118553d72cc499046
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47726145"
---
# <a name="keyset-cursors"></a>键集游标
键集游标提供静态和动态游标之间的功能的功能，以检测更改。 如静态游标，它不会不始终检测到更改的成员身份和顺序的结果集。 类似动态游标，它检测到的行值发生更改的结果集中。  
  
 由键集驱动的游标控制的一组称为键集的唯一标识符 （键）。 键是根据以唯一方式标识结果集中各行的一组列生成的。 由键集是从返回的查询语句的所有行的键值的组。  
  
 使用由键集驱动的游标，密钥生成和保存游标中的每一行并存储客户端工作站或服务器上。 在访问每个行时，存储的密钥可用来从数据源提取当前数据值。 在由键集驱动的游标，结果集的成员身份被冻结时已完全填充由键集。 此后，添加内容或更新会影响成员身份不是结果集之前重新打开它的一部分。  
  
 因为在用户滚动浏览结果集，会显示为 （使其通过由键集所有者或其他进程） 的数据值的更改。 （由其他进程） 游标外部所做的插入是可见的仅当关闭并重新打开游标。 从游标内部进行的插入是结果集的末尾可见。  
  
 如果由键集驱动游标试图来检索已删除的行，行显示为一个"hole"的结果集中。 行的键存在于由键集，但在结果集中不存在的行。 如果更新某一行中的密钥值，则将该行视为已删除和然后插入，因此这样的行也将显示为结果集中的孔。 由键集驱动游标始终可以检测到其他进程中删除的行，尽管它可以选择删除它将自身删除的行的键。 执行此操作的由键集驱动游标无法检测到自己的删除，因为已删除的证据。  
  
 对键列的更新与删除旧密钥后再插入新项的操作。 新键值不是不通过游标进行更新时可见的。 如果通过游标进行更新，新密钥值是结果集的末尾可见。  
  
 没有名为由键集驱动标准游标键集驱动游标的变体。 由键集驱动的标准光标，在结果集中的行的成员身份和行的顺序固定的游标打开时，但对值由游标所有者所做的更改和其他进程提交的更改是可见。 如果更改将使成员身份的行，或者会影响行的顺序，行不会消失或移动，除非关闭并重新打开游标。 插入的数据未显示，但对现有数据的更改并出现和在提取行。  
  
 由键集驱动游标很难正确使用数据的更改敏感度取决于许多不同的情况下，因为如上文所述。 但是，如果你的应用程序不关心并发更新，可以以编程方式处理错误的键，并且必须直接访问某些键的行，由键集驱动游标可能适用于您。 使用**adOpenKeyset CursorTypeEnum**以指示你想要使用在 ADO 中的键集游标。  
  
## <a name="see-also"></a>请参阅  
 [只进游标](../../../ado/guide/data/forward-only-cursors.md)   
 [静态游标](../../../ado/guide/data/static-cursors.md)   
 [动态游标](../../../ado/guide/data/dynamic-cursors.md)
