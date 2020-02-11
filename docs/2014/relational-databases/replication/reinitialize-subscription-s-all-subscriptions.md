---
title: 重新初始化订阅 - 所有订阅 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.reinit.all.f1
helpviewer_keywords:
- Reinitialize Subscription(s) dialog box
ms.assetid: e1122018-9f74-43e3-8489-7eae33ff23d9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8bcd42996ee35839162ee4e541f5be44c2d602aa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63131501"
---
# <a name="reinitialize-subscriptions---all-subscriptions"></a>重新初始化订阅 - 所有订阅
  使用 **“重新初始化订阅”** 对话框，可以将发布的所有订阅都标记为需要重新初始化。 重新初始化涉及向每个订阅服务器应用快照；对于事务发布的订阅，这是由分发代理执行的，而对于合并发布的订阅，这是由合并代理执行的。  
  
## <a name="options"></a>选项  
 **使用当前快照**  
 选择此选项可以在下一次为订阅运行分发代理或合并代理时将当前快照应用于每个订阅服务器。 如果无法获得有效快照，将无法选定此选项。  
  
 **使用新快照**  
 选择此选项可以用新快照重新初始化所有订阅。 只有在快照代理生成快照之后，才能将快照应用于每个订阅服务器。 如果将快照代理设置为按计划运行，则只有在快照代理按计划下一次运行之后，才会重新初始化订阅。  
  
 选择 **“立即生成新快照”** 可以立即启动快照代理。  
  
 **在重新初始化之前上载未同步的更改**  
 仅限合并复制。 选择此选项可以在用快照覆盖订阅服务器上的数据之前，从订阅数据库上载所有挂起的更改。  
  
 如果添加、删除或更改参数化筛选器，则订阅服务器上挂起的更改在重新初始化期间将无法上载到发布服务器。 若要上载挂起的更改，请在更改筛选器前同步所有订阅。  
  
 **标记为要重新初始化**  
 单击此项可以将每个订阅标记为需要重新初始化。 在可以获得有效快照后，下次为订阅运行分发代理或合并代理时，该快照将应用在订阅服务器上。  
  
## <a name="see-also"></a>另请参阅  
 [重新初始化订阅](reinitialize-subscriptions.md)  
  
  
