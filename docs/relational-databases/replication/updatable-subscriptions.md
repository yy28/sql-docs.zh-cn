---
title: 可更新订阅 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.updatablesubscriptions.f1
ms.assetid: 8e9a13a0-6b24-47c6-9d83-3cbaf08f673d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d11def4fcc53c656c7b04679d4f3373e5eb2557b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47781065"
---
# <a name="updatable-subscriptions"></a>可更新订阅
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  如果使用的是事务复制，应将复制的数据视为只读数据；不过，可以使用可更新的订阅，在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器上修改复制的数据。 如果需要在订阅服务器上修改数据，请根据您的要求选择下列选项之一。  
  
|可更新订阅类型|要求|  
|---------------------------------|------------------|  
|立即更新|必须连接发布服务器和订阅服务器才能更新订阅服务器上的数据。|  
|排队更新|不必连接发布服务器和订阅服务器即可更新订阅服务器上的数据。 可以在脱机状态下进行更新，之后还可以在发布服务器与订阅服务器之间同步更新。|  
  
## <a name="options"></a>选项  
 **复制订阅服务器更改**  
 对于每个应该能够进行更新的订阅服务器，选中 **“复制”** 列中的复选框。 对于能够进行更新的订阅服务器，请从 **“在发布服务器提交”** 列的下拉列表框中选择相应的选项：  
  
-   对于立即更新订阅，请选择 **“同时提交更改”** 。  
  
-   对于排队更新订阅，请选择 **“对更改进行排队并在可能时提交”** 。  
  
## <a name="see-also"></a>另请参阅  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
