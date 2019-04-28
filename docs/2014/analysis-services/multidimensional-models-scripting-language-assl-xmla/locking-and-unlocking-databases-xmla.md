---
title: 锁定和解锁数据库 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- locking [XML for Analysis]
- XML for Analysis, locking
- XMLA, locking
- unlocking objects
ms.assetid: 451afa58-ce03-4ecc-8dd3-9e7e8559b5f1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 290f1e5fe7efb876ab6c24004c7465cf109de0d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62702231"
---
# <a name="locking-and-unlocking-databases-xmla"></a>锁定数据库和解除数据库锁定 (XMLA)
  可以锁定和解锁分别使用的数据库，则[锁](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)并[解锁](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)XML for Analysis (XMLA) 中的命令。 通常，其他 XMLA 命令会在执行期间根据需要自动锁定对象和解除对象锁定，从而完成命令。 您可以显式锁定或解锁数据库以执行在单个事务中的多个命令，如[批处理](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)命令，同时防止其他应用程序提交到数据库的写入事务。  
  
## <a name="locking-databases"></a>锁定数据库  
 `Lock` 命令锁定当前活动事务上下文中的对象，该锁可为共享锁或排他锁。 对象上的锁将阻止提交事务，直到删除该锁为止。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持两种类型的锁： 共享的锁和排他锁。 有关支持的锁类型的详细信息[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，请参阅[Mode 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/mode-element-xmla)。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 仅允许锁定数据库。 [对象](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)元素必须包含的对象引用[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。 如果未指定 `Object` 元素或 `Object` 元素引用数据库以外的对象，则将引发错误。  
  
> [!IMPORTANT]  
>  只有数据库管理员或服务器管理员可以显式发出 `Lock` 命令。  
  
 其他命令将对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库隐式发出 `Lock` 命令。 从一个数据库，例如任何读取数据或元数据的任何操作[Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)方法或[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法运行[语句](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla)命令，隐式发出一个共享对数据库锁定。 提交数据或元数据中的更改的对象上的任何事务[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库，例如`Execute`方法运行[Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)命令，隐式发出对数据库的排他锁。  
  
## <a name="unlocking-objects"></a>解锁对象  
 `Unlock` 命令可删除在当前活动事务的上下文中建立的锁。  
  
> [!IMPORTANT]  
>  只有数据库管理员或服务器管理员可以显式发出`Unlock`命令。  
  
 所有锁都位于当前事务的上下文中。 当提交或回滚当前事务时，事务中定义的所有锁都将自动释放。  
  
## <a name="see-also"></a>请参阅  
 [锁定元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [Unlock 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  
