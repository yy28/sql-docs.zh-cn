---
title: 锁定数据库和解除数据库锁定（XMLA） |Microsoft Docs
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
ms.openlocfilehash: 96afa94f7c9c20072ae88b09a436d079ce0478ae
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544987"
---
# <a name="locking-and-unlocking-databases-xmla"></a>锁定数据库和解除数据库锁定 (XMLA)
  您可以分别使用 XML for Analysis （XMLA）中的 "[锁定](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)" 和 "[解锁](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)" 命令锁定和解锁数据库。 通常，其他 XMLA 命令会在执行期间根据需要自动锁定对象和解除对象锁定，从而完成命令。 可以显式锁定或解锁数据库，以便在单个事务中执行多个命令，例如[批处理](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)命令，同时防止其他应用程序将写入事务提交到数据库。  
  
## <a name="locking-databases"></a>锁定数据库  
 `Lock` 命令锁定当前活动事务上下文中的对象，该锁可为共享锁或排他锁。 对象上的锁将阻止提交事务，直到删除该锁为止。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持两种类型的锁：共享锁和排他锁。 有关支持的锁类型的详细信息 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，请参阅[Mode 元素 &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/mode-element-xmla)。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 仅允许锁定数据库。 [Object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)元素必须包含对数据库的对象引用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 。 如果未指定 `Object` 元素或 `Object` 元素引用数据库以外的对象，则将引发错误。  
  
> [!IMPORTANT]  
>  只有数据库管理员或服务器管理员可以显式发出 `Lock` 命令。  
  
 其他命令将对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库隐式发出 `Lock` 命令。 任何从数据库读取数据或元数据的操作（例如任何[发现](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)方法或运行[语句](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla)命令的[Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)方法）都隐式发出数据库上的共享锁。 将数据或元数据的更改提交到数据库中的对象（ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 例如 `Execute` 运行[Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)命令的方法）的任何事务都隐式发出数据库上的排他锁。  
  
## <a name="unlocking-objects"></a>解锁对象  
 `Unlock` 命令可删除在当前活动事务的上下文中建立的锁。  
  
> [!IMPORTANT]  
>  只有数据库管理员或服务器管理员可以显式发出 `Unlock` 命令。  
  
 所有锁都位于当前事务的上下文中。 当提交或回滚当前事务时，事务中定义的所有锁都将自动释放。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;XMLA&#41;锁定元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [&#40;XMLA&#41;解锁元素](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  
