---
title: MSSQLSERVER_41399 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41399 (Database Engine error)
ms.assetid: 5e5acb07-16ca-4329-8210-cd2bab0c904f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1e1243d12083005bb2fa553970cc0f3ebf2dd18a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "68123122"
---
# <a name="mssqlserver_41399"></a>MSSQLSERVER_41399
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|41399|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|MAX_SORT_ROW_WIDTH_EXCEEDED|  
|消息正文|排序操作太复杂。 有关详细信息，请查阅 SQL Server 联机丛书。|  
  
## <a name="explanation"></a>说明  
对联接和聚合操作的结果进行排序会通过增加排序缓冲区中行的大小而增加排序操作的复杂程度。 此错误意味着行的大小大于本机编译存储过程中排序运算符支持的最大大小。 请注意，排序缓冲区中行的大小只由联接的数目以及聚合函数的数目和类型确定。 基表中行的大小不会影响排序缓冲区中行的大小。  
  
## <a name="user-action"></a>用户操作  
通过删除联接或聚合函数降低查询的复杂程度。  
  
## <a name="see-also"></a>另请参阅  
[内存中 OLTP（内存中优化）](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
