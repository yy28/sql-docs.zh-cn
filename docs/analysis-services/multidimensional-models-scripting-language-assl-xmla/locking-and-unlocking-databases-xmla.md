---
title: 锁定和解锁数据库 (XMLA) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d9868b251ff95fae1822abb5844ff7e909940dae
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34024774"
---
# <a name="locking-and-unlocking-databases-xmla"></a>锁定数据库和解除数据库锁定 (XMLA)
  你可以锁定和解锁分别使用的数据库，则[锁](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)和[解锁](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)XML Analysis (XMLA) 中的命令。 通常，其他 XMLA 命令会在执行期间根据需要自动锁定对象和解除对象锁定，从而完成命令。 你可以显式锁定或解锁数据库执行多个命令在单个事务中，如[批处理](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)命令，同时防止从提交到数据库写入事务的其他应用程序。  
  
## <a name="locking-databases"></a>锁定数据库  
 **锁**命令锁定的对象，供共享或独占使用，在当前活动事务的上下文中。 对象上的锁将阻止提交事务，直到删除该锁为止。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持两种类型的锁、 共享的锁和排他锁。 有关支持的锁类型的详细信息[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，请参阅[模式元素 & #40;XMLA & #41;](../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md).  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 仅允许锁定数据库。 [对象](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)元素必须包含对的对象引用[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。 如果**对象**未指定元素或如果**对象**元素引用数据库之外的对象将会出错。  
  
> [!IMPORTANT]  
>  只有数据库管理员或服务器管理员可以显式发出**锁**命令。  
  
 其他的隐式命令问题**锁**命令[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。 从数据库，如任何中读取数据或元数据的任何操作[发现](../../analysis-services/xmla/xml-elements-methods-discover.md)方法或[执行](../../analysis-services/xmla/xml-elements-methods-execute.md)运行方法[语句](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)命令，隐式颁发共享锁定数据库上。 将数据或元数据中的更改提交到一个对象，在任何事务[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库，如**执行**运行方法[Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)命令，隐式上发出的排他锁数据库。  
  
## <a name="unlocking-objects"></a>解锁的对象  
 **Unlock** 命令可删除在当前活动事务的上下文中建立的锁。  
  
> [!IMPORTANT]  
>  只有数据库管理员或服务器管理员可以显式发出 **Unlock** 命令。  
  
 所有锁都位于当前事务的上下文中。 当提交或回滚当前事务时，事务中定义的所有锁都将自动释放。  
  
## <a name="see-also"></a>另请参阅  
 [锁定元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)   
 [解锁元素 & #40;XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)   
 [使用 Analysis Services 中的 XMLA 进行开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
