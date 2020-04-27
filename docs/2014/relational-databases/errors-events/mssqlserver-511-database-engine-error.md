---
title: MSSQLSERVER_511 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 511 (Database Engine error)
ms.assetid: 0c85686a-53c1-4180-ba8c-2000e68a0d63
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ee53135fb492185d91287f553b7b1f0ddf3cc8ba
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62867792"
---
# <a name="mssqlserver_511"></a>MSSQLSERVER_511
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|511|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|ROW_TOOBIG|  
|消息正文|不能创建大小为 %d 的行，该大小大于所允许的最大值 %d。|  
  
## <a name="explanation"></a>说明  
 尝试的操作已超出行大小的最大值。 通常，行大小的最大值为 8,060 个字节。 某些存储格式包含的开销可减小数据可用的行大小。 例如，使用稀疏列时，行大小的最大值为 8,018 个字节。 某些添加或删除行的操作和某些更改列的数据类型的操作要求在数据页重写此行，然后才能删除原始行。 在这些操作中，行大小的有效限制值为最大限制值的一半。 这是因为，在短时间内，原始行和已修改的行都必须保留在数据页中。  
  
> [!WARNING]  
>  每个非 null **varchar （max）** 或**nvarchar （max）** 列都需要24个字节的附加固定分配，该分配在排序操作期间针对8060字节行限制进行计数。 这可以为表中可创建的非 null **varchar （max）** 或**nvarchar （max）** 列数创建隐式限制。 在以下情况下不提供特殊错误：创建表格（最大行大小超过允许的最大 8060 字节时出现的一般警告除外）时，或插入数据时。 这一较大的行大小可能会导致在执行某些正常操作（例如聚集索引键更新或完整列集排序）期间出现错误（例如错误 512），使得用户在执行操作前无法预料到此类错误。  
  
## <a name="user-action"></a>用户操作  
 如果可能，请减小该行的大小。  
  
 如果您认为此问题是由对该行进行就地更新引起，则必须采用多个步骤更改此表。 创建一个新表，并将数据传输到此新表中。 然后，或者删除原始表并重命名此新表，或者截断原始表，修改原始表中的行，然后将数据重新移到原始表中。  
  
  
