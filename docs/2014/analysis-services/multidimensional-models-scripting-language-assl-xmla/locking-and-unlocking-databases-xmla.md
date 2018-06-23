---
title: 锁定和解锁数据库 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- locking [XML for Analysis]
- XML for Analysis, locking
- XMLA, locking
- unlocking objects
ms.assetid: 451afa58-ce03-4ecc-8dd3-9e7e8559b5f1
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: dbcf03fee7b0b286a88c4c3089f42741e60dbff0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130239"
---
# <a name="locking-and-unlocking-databases-xmla"></a>锁定数据库和解除数据库锁定 (XMLA)
  你可以锁定和解锁分别使用的数据库，则[锁](../xmla/xml-elements-commands/lock-element-xmla.md)和[解锁](../xmla/xml-elements-commands/unlock-element-xmla.md)XML Analysis (XMLA) 中的命令。 通常，其他 XMLA 命令会在执行期间根据需要自动锁定对象和解除对象锁定，从而完成命令。 你可以显式锁定或解锁数据库执行多个命令在单个事务中，如[批处理](../xmla/xml-elements-commands/batch-element-xmla.md)命令，同时防止从提交到数据库写入事务的其他应用程序。  
  
## <a name="locking-databases"></a>锁定数据库  
 `Lock` 命令锁定当前活动事务上下文中的对象，该锁可为共享锁或排他锁。 对象上的锁将阻止提交事务，直到删除该锁为止。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持两种类型的锁、 共享的锁和排他锁。 有关支持的锁类型的详细信息[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，请参阅[模式元素&#40;XMLA&#41;](../xmla/xml-elements-properties/mode-element-xmla.md)。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 仅允许锁定数据库。 [对象](../xmla/xml-elements-properties/object-element-xmla.md)元素必须包含对的对象引用[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。 如果未指定 `Object` 元素或 `Object` 元素引用数据库以外的对象，则将引发错误。  
  
> [!IMPORTANT]  
>  只有数据库管理员或服务器管理员可以显式发出 `Lock` 命令。  
  
 其他命令将对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库隐式发出 `Lock` 命令。 从数据库，如任何中读取数据或元数据的任何操作[发现](../xmla/xml-elements-methods-discover.md)方法或[执行](../xmla/xml-elements-methods-execute.md)运行方法[语句](../xmla/xml-elements-commands/statement-element-xmla.md)命令，隐式颁发共享锁定数据库上。 将数据或元数据中的更改提交到一个对象，在任何事务[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库，如`Execute`运行方法[Alter](../xmla/xml-elements-commands/alter-element-xmla.md)命令，隐式发出数据库上的排他锁。  
  
## <a name="unlocking-objects"></a>解锁的对象  
 `Unlock` 命令可删除在当前活动事务的上下文中建立的锁。  
  
> [!IMPORTANT]  
>  只有数据库管理员或服务器管理员可以显式发出`Unlock`命令。  
  
 所有锁都位于当前事务的上下文中。 当提交或回滚当前事务时，事务中定义的所有锁都将自动释放。  
  
## <a name="see-also"></a>请参阅  
 [锁定元素&#40;XMLA&#41;](../xmla/xml-elements-commands/lock-element-xmla.md)   
 [解除锁定元素&#40;XMLA&#41;](../xmla/xml-elements-commands/unlock-element-xmla.md)   
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  