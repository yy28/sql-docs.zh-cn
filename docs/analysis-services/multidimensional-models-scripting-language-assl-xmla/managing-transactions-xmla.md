---
title: 管理事务 (XMLA) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1f2884d49f03d8557d72d8d6d48cdba432a8c37f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="managing-transactions-xmla"></a>管理事务 (XMLA)
  每个 XML for Analysis (XMLA) 命令发送到的实例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]上当前的隐式或显式会话事务的上下文中运行。 若要管理每个这些事务，你可以使用[BeginTransaction](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)， [CommitTransaction](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)，和[RollbackTransaction](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)命令。 通过使用这些命令，可创建隐式或显式事务，更改事务引用计数以及启动、提交或回滚事务。  
  
## <a name="implicit-and-explicit-transactions"></a>隐式和显式事务  
 事务可以是隐式的或显式的：  
  
 **隐式事务**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 创建*隐式*事务的 XMLA 命令如果**BeginTransaction**命令未指定启动事务。 如果此命令成功，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将始终提交隐式事务，如果此命令失败，则将回滚隐式事务。  
  
 **显式事务**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 创建*显式*事务如果**BeginTransaction**命令启动的事务。 但是，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]仅提交的显式事务，如果**CommitTransaction**命令被发送，而如果回退显式事务**RollbackTransaction**发送命令。  
  
 此外，如果在活动事务完成之前，当前事务结束，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将同时回滚隐式事务和显式事务。  
  
## <a name="transactions-and-reference-counts"></a>事务和引用计数  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可继续每个会话的事务引用计数。 但是，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 不支持嵌套事务，因为仅为每个会话维持一个活动事务。 如果当前会话没有活动事务，则事务引用计数将设置为零。  
  
 换而言之，每个**BeginTransaction**命令递增 1 引用计数，而每个**CommitTransaction**命令递减引用计数 1。 如果**CommitTransaction**命令将事务计数设置为零，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提交事务。  
  
 但是， **RollbackTransaction**命令回滚活动事务而不考虑当前值的事务的引用计数。 换而言之，单个**RollbackTransaction**命令回滚活动事务，无论多少**BeginTransaction**命令或**CommitTransaction**命令已发送并设置事务的引用计数为零。  
  
## <a name="beginning-a-transaction"></a>开始事务  
 **BeginTransaction**命令开始在当前会话的显式事务，并递增 1 事务引用计数为当前会话。 所有后续命令被认为是在活动事务中，直到足够**CommitTransaction**发送命令以提交活动事务或单个**RollbackTransaction**发送命令回滚活动事务。  
  
## <a name="committing-a-transaction"></a>提交事务  
 **CommitTransaction**命令提交的后运行的命令的结果**BeginTransaction**命令已在当前会话上运行。 每个**CommitTransaction**递减的活动事务的引用计数命令的会话。 如果**CommitTransaction**命令将引用计数设置为零，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提交活动事务。 如果没有活动事务 （换而言之，当前会话的事务引用计数已设置为零）， **CommitTransaction**命令导致错误。  
  
## <a name="rolling-back-a-transaction"></a>回滚事务  
 **RollbackTransaction**命令回滚的后运行的命令的结果**BeginTransaction**命令已在当前会话上运行。 **RollbackTransaction**命令回滚活动事务，而不考虑当前事务的引用计数，并将事务的引用计数设置为零。 如果没有活动事务 （换而言之，当前会话的事务引用计数已设置为零）， **RollbackTransaction**命令导致错误。  
  
## <a name="see-also"></a>另请参阅  
 [使用 Analysis Services 中的 XMLA 进行开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
