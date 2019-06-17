---
title: 重新初始化订阅 - 一个订阅 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.reinit.single.f1
helpviewer_keywords:
- Reinitialize Subscription(s) dialog box
ms.assetid: 9b0cf0be-d1f1-4163-a0ca-d6f095aa707e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: af1548ad29203f06e6d9cc49c048f1973afa3e3b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63131465"
---
# <a name="reinitialize-subscriptions---one-subscription"></a>重新初始化订阅 - 一个订阅
  可以使用 **“重新初始化订阅”** 对话框标记需要重新初始化的订阅。 重新初始化会涉及将快照应用于订阅服务器；对于事务发布的订阅，是由分发代理执行的；而对于合并发布的订阅，则是由合并代理执行的。  
  
## <a name="options"></a>选项  
 **使用当前快照**  
 选择此项可以在分发代理或合并代理下一次运行时将当前快照应用于订阅服务器。 如果无法获得有效快照，将无法选定此选项。  
  
 **使用新快照**  
 选择此项可以用新的快照来重新初始化订阅。 只有在快照代理已经生成新快照之后，才能将其应用于订阅服务器。 如果将快照代理设置为按计划运行，则只有到下一次运行计划快照代理之后，才会重新初始化订阅。  
  
 选择 **“立即生成新快照”** 可以立即启动快照代理。  
  
 **在重新初始化之前上载未同步的更改**  
 仅限合并复制。 选择此项可以在用快照覆盖订阅服务器上的数据之前，从订阅数据库上载任何挂起的更改。  
  
 如果添加、删除或更改参数化筛选器，则订阅服务器上挂起的更改在重新初始化期间将无法上载到发布服务器。 若要上载挂起的更改，请在更改筛选器前同步所有订阅。  
  
 **标记为要重新初始化**  
 单击此项可以标记需要重新初始化的订阅。 在可以获得有效快照后，下次为订阅运行分发代理或合并代理时，该快照将应用在订阅服务器上。  
  
## <a name="see-also"></a>请参阅  
 [重新初始化订阅](reinitialize-subscriptions.md)  
  
  
