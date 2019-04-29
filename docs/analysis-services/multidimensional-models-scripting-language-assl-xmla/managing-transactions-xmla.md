---
title: 管理事务 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c85b1f9db4667c64bed7cf87189e48b507e5f75
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63055072"
---
# <a name="managing-transactions-xmla"></a>管理事务 (XMLA)
  每个 XML for Analysis (XMLA) 命令发送到的实例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]上当前的隐式或显式会话的事务的上下文中运行。 若要管理每个这些事务，您可以使用[BeginTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/begintransaction-element-xmla)， [CommitTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/committransaction-element-xmla)，并[RollbackTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/rollbacktransaction-element-xmla)命令。 通过使用这些命令，可创建隐式或显式事务，更改事务引用计数以及启动、提交或回滚事务。  
  
## <a name="implicit-and-explicit-transactions"></a>隐式和显式事务  
 事务可以是隐式的或显式的：  
  
 **隐式事务**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 创建*隐式*为 xmla 命令的命令**BeginTransaction**命令未指定启动事务。 如果此命令成功，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将始终提交隐式事务，如果此命令失败，则将回滚隐式事务。  
  
 **显式事务**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 创建*显式*事务如果**BeginTransaction**命令启动的事务。 但是，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]仅提交显式事务，如果**CommitTransaction**命令被发送，而如果回滚显式事务**RollbackTransaction**发送命令。  
  
 此外，如果在活动事务完成之前，当前事务结束，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将同时回滚隐式事务和显式事务。  
  
## <a name="transactions-and-reference-counts"></a>事务和引用计数  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可继续每个会话的事务引用计数。 但是，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 不支持嵌套事务，因为仅为每个会话维持一个活动事务。 如果当前会话没有活动事务，则事务引用计数将设置为零。  
  
 换而言之，每个**BeginTransaction**命令递增引用计数 1，而每个**CommitTransaction**命令递减引用计数按 1。 如果**CommitTransaction**命令将事务计数设置为零，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提交事务。  
  
 但是， **RollbackTransaction**命令回滚活动事务而不考虑当前值的事务引用计数。 换而言之，单个**RollbackTransaction**命令回滚活动事务，无论多少**BeginTransaction**命令或**CommitTransaction**命令发送了，并设置事务引用计数为零。  
  
## <a name="beginning-a-transaction"></a>开始事务  
 **BeginTransaction**命令开始在当前会话上的显式事务，并由一个递增当前会话的事务引用计数。 所有后续命令都将视为都在活动事务中，直至足够**CommitTransaction**发送命令以提交活动事务或将单个**RollbackTransaction**发送命令回滚活动事务。  
  
## <a name="committing-a-transaction"></a>提交事务  
 **CommitTransaction**命令提交后运行的命令的结果**BeginTransaction**当前会话运行命令。 每个**CommitTransaction**命令都会减少会话上的活动事务的引用计数。 如果**CommitTransaction**命令将引用计数设置为零，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]提交活动事务。 如果没有活动事务 （即，当前会话的事务引用计数已设置为零）， **CommitTransaction**命令将导致错误。  
  
## <a name="rolling-back-a-transaction"></a>回滚事务  
 **RollbackTransaction**命令回滚后运行的命令的结果**BeginTransaction**当前会话运行命令。 **RollbackTransaction**命令回滚活动事务，而不考虑当前事务引用计数，并将事务引用计数设置为零。 如果没有活动事务 （即，当前会话的事务引用计数已设置为零）， **RollbackTransaction**命令将导致错误。  
  
## <a name="see-also"></a>请参阅  
 [在 Analysis Services 中使用 XMLA 开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
