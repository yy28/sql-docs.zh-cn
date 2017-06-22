---
title: MSSQLSERVER_511 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 511 (Database Engine error)
ms.assetid: 0c85686a-53c1-4180-ba8c-2000e68a0d63
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6f1ef308a5c84a9c0bdee065c67fcc3328798136
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver511"></a>MSSQLSERVER_511
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|511|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|ROW_TOOBIG|  
|消息正文|不能创建大小为 %d 的行，该大小大于所允许的最大值 %d。|  
  
## <a name="explanation"></a>解释  
尝试的操作已超出行大小的最大值。 通常，行大小的最大值为 8,060 个字节。 某些存储格式包含的开销可减小数据可用的行大小。 例如，使用稀疏列时，行大小的最大值为 8,018 个字节。 某些添加或删除行的操作和某些更改列的数据类型的操作要求在数据页重写此行，然后才能删除原始行。 在这些操作中，行大小的有效限制值为最大限制值的一半。 这是因为，在短时间内，原始行和已修改的行都必须保留在数据页中。  
  
## <a name="user-action"></a>用户操作  
如果可能，请减小该行的大小。  
  
如果您认为此问题是由对该行进行就地更新引起，则必须采用多个步骤更改此表。 创建一个新表，并将数据传输到此新表中。 然后，或者删除原始表并重命名此新表，或者截断原始表，修改原始表中的行，然后将数据重新移到原始表中。  
  

