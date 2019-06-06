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
manager: jroth
ms.openlocfilehash: b349838788a3c442ea9c32fc5b8a7ebbd0240e37
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702084"
---
# <a name="keyset-cursors"></a>键集游标
键集游标提供静态和动态游标之间的功能的功能，以检测更改。 比如静态游标，它不会始终检测对结果集的成员身份和顺序的更改。 比如动态游标，它会检测对结果集中的行值的更改。  
  
 由键集驱动的游标由一组唯一标识符（键）控制，这组键称为键集。 键是根据以唯一方式标识结果集中各行的一组列生成的。 键集是查询语句返回的所有行中的一组键值。  
  
 使用由键集驱动的游标，为游标中的每行生成和保存一个键，并将其存储在客户端工作站或服务器上。 访问每行时，存储的密钥可用来从数据源提取当前数据值。 在由键集驱动的游标中，如果键集完全填充，将冻结结果集成员身份。 此后，在重新打开结果集前，都不会执行影响成员身份的添加或更新操作。  
  
 因为在用户滚动浏览结果集，会显示为 （使其通过由键集所有者或其他进程） 的数据值的更改。 游标外所做的插入（由其他进程执行）仅在关闭并重新打开游标后可见。 游标内部所做的插入在结果集的末尾可见。  
  
 如果由键集驱动游标试图来检索已删除的行，行显示为一个"hole"的结果集中。 行键存在于键集中，但行不再存在于结果集中。 如果更新某一行中的密钥值，则将该行视为已删除和然后插入，因此这样的行也将显示为结果集中的孔。 由键集驱动游标始终可以检测到其他进程中删除的行，尽管它可以选择删除它将自身删除的行的键。 执行此操作的由键集驱动游标无法检测到自己的删除，因为已删除的证据。  
  
 对键列的更新与删除旧密钥后再插入新项的操作。 新键值不是不通过游标进行更新时可见的。 如果通过游标进行更新，新密钥值是结果集的末尾可见。  
  
 没有名为由键集驱动标准游标键集驱动游标的变体。 由键集驱动的标准光标，在结果集中的行的成员身份和行的顺序固定的游标打开时，但对值由游标所有者所做的更改和其他进程提交的更改是可见。 如果更改将使成员身份的行，或者会影响行的顺序，行不会消失或移动，除非关闭并重新打开游标。 插入的数据未显示，但对现有数据的更改并出现和在提取行。  
  
 由键集驱动游标很难正确使用数据的更改敏感度取决于许多不同的情况下，因为如上文所述。 但是，如果你的应用程序不关心并发更新，可以以编程方式处理错误的键，并且必须直接访问某些键的行，由键集驱动游标可能适用于您。 使用**adOpenKeyset CursorTypeEnum**以指示你想要使用在 ADO 中的键集游标。  
  
## <a name="see-also"></a>请参阅  
 [只进游标](../../../ado/guide/data/forward-only-cursors.md)   
 [静态游标](../../../ado/guide/data/static-cursors.md)   
 [动态游标](../../../ado/guide/data/dynamic-cursors.md)
