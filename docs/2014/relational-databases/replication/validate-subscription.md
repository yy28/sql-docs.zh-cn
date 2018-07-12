---
title: 验证单个订阅 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.validate.validateandresynch.f1
helpviewer_keywords:
- Validate Subscription dialog box
ms.assetid: 74bdf5e1-b886-4284-b5fb-332bf79ae083
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ee7484c14705bdd98bbfd28283eb20971c51f580
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37154228"
---
# <a name="validate-subscription"></a>验证单个订阅
  可以使用 **“验证单个订阅”** 对话框，指定在下次运行订阅的合并代理时应对针对合并发布的订阅进行验证。 验证的结果显示在复制监视器中。 有关详细信息，请参阅 [Validate Data at the Subscriber](validate-data-at-the-subscriber.md)。  
  
 也可以在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中右键单击某个发布，并单击 **“验证所有订阅”** 来验证对合并发布的所有订阅。  
  
## <a name="options"></a>“常规”  
 **上次尝试验证的日期**  
 最后一个包含订阅验证（无论验证是否成功）的合并代理会话的日期。  
  
 **上次成功验证的日期**  
 最后一个包含成功订阅验证的合并代理会话的日期。  
  
 **验证此订阅**  
 选择此选项可验证订阅。  
  
 **选项**  
 单击此项可访问 **“订阅验证选项”** 对话框，使用此对话框可以指定是使用行计数验证还是使用二进制校验和验证。  
  
## <a name="see-also"></a>请参阅  
 [验证已复制的数据](validate-replicated-data.md)  
  
  
