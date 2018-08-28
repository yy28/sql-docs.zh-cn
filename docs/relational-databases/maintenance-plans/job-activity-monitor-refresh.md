---
title: 作业活动监视器刷新 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: maintenance-plans
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.jobactivitymon.refresh.f1
ms.assetid: 413a368e-fd2b-4e1f-b370-002cdbc85bab
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 52160a10a8b404588103f36c90a103f9067530ba
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40410969"
---
# <a name="job-activity-monitor-refresh"></a>作业活动监视器刷新
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用 **“刷新设置”** 对话框可以配置作业活动监视器获取服务器活动最新信息的频率。 作业活动监视器必须对所监视的服务器运行查询才能获取作业活动监视器网格的信息。 当自动刷新间隔设置为小于 30 秒时，运行这些查询所用的时间可能会影响服务器性能。  
  
 若要打开此对话框，请在作业活动监视器的 **“状态”** 部分中单击 **“查看刷新设置”** 。  
  
## <a name="options"></a>选项  
 **自动刷新间隔**  
 选中此选项将启动活动监视器信息的自动刷新功能。 默认情况下，此功能为关闭状态。  
  
 **seconds**  
 自动刷新的间隔秒数。 默认值为 60 秒。 当设置为 5 秒或小于 5 秒时，则每隔 5 秒刷新一次。  
  
## <a name="see-also"></a>另请参阅  
 [监视作业活动](../../ssms/agent/monitor-job-activity.md)  
  
  
