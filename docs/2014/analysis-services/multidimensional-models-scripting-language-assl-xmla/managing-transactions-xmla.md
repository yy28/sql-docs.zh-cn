---
title: 管理事务 (XMLA) |Microsoft Docs
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
- XML for Analysis, transactions
- XMLA, transactions
- explicit transactions [XMLA]
- implicit transactions
- transactions [XML for Analysis]
- rolling back transactions, XMLA
- reference counts [XML for Analysis]
- committing transactions
- starting transactions
ms.assetid: f5112e01-82f8-4870-bfb7-caa00182c999
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fefda354d9f596c92a06673e7692bb840f582071
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167608"
---
# <a name="managing-transactions-xmla"></a>管理事务 (XMLA)
  每个 XML for Analysis (XMLA) 命令发送到的实例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]上当前的隐式或显式会话的事务的上下文中运行。 若要管理每个这些事务，您可以使用[BeginTransaction](../xmla/xml-elements-commands/begintransaction-element-xmla.md)， [CommitTransaction](../xmla/xml-elements-commands/committransaction-element-xmla.md)，并[RollbackTransaction](../xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)命令。 通过使用这些命令，可创建隐式或显式事务，更改事务引用计数以及启动、提交或回滚事务。  
  
## <a name="implicit-and-explicit-transactions"></a>隐式和显式事务  
 事务可以是隐式的或显式的：  
  
 **隐式事务**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 创建*隐式*为 xmla 命令的命令`BeginTransaction`命令未指定启动事务。 如果此命令成功，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将始终提交隐式事务，如果此命令失败，则将回滚隐式事务。  
  
 **显式事务**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 创建*显式*事务如果`BeginTransaction`命令启动的事务。 但是，如果发送 `CommitTransaction` 命令，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 仅提交显式事务，如果发送 `RollbackTransaction` 命令，则将回滚显式事务。  
  
 此外，如果在活动事务完成之前，当前事务结束，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将同时回滚隐式事务和显式事务。  
  
## <a name="transactions-and-reference-counts"></a>事务和引用计数  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可继续每个会话的事务引用计数。 但是，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 不支持嵌套事务，因为仅为每个会话维持一个活动事务。 如果当前会话没有活动事务，则事务引用计数将设置为零。  
  
 换言之，每个 `BeginTransaction` 命令使引用计数按 1 递增，而每个 `CommitTransaction` 命令使引用计数按 1 递减。 如果 `CommitTransaction` 命令将事务计数设置为零，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将提交该事务。  
  
 但是，无论事务引用计数的当前值如何，`RollbackTransaction` 命令都将回滚活动事务。 换言之，不管已发送多少 `RollbackTransaction` 命令或 `BeginTransaction` 命令，单个 `CommitTransaction` 命令都将回滚活动事务，并将事务引用计数设置为零。  
  
## <a name="beginning-a-transaction"></a>开始事务  
 `BeginTransaction` 命令可在当前会话上开始显式事务，并按 1 递增当前会话的事务引用计数。 所有后续命令都将视为位于活动事务中，直至发送足够的 `CommitTransaction` 命令来提交活动事务，或发送单个 `RollbackTransaction` 命令来回滚活动事务。  
  
## <a name="committing-a-transaction"></a>提交事务  
 `CommitTransaction` 命令可提交对当前会话运行 `BeginTransaction` 命令后运行的命令的结果。 每个 `CommitTransaction` 命令都会减少会话上活动事务的引用计数。 如果 `CommitTransaction` 命令将引用计数设置为零，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将提交活动事务。 如果不存在活动事务（换言之，当前会话的事务引用计数已设置为零），则 `CommitTransaction` 命令将导致出错。  
  
## <a name="rolling-back-a-transaction"></a>回滚事务  
 `RollbackTransaction` 命令可回滚对当前会话运行 `BeginTransaction` 命令后运行的命令的结果。 无论当前事务引用计数如何，`RollbackTransaction` 命令都将回滚活动事务，并将事务引用计数设置为零。 如果不存在活动事务（换言之，当前会话的事务引用计数已设置为零），则 `RollbackTransaction` 命令将导致出错。  
  
## <a name="see-also"></a>请参阅  
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  
