---
title: 任务9：配置引用数据服务 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d0535fce-2bf5-4f6d-b517-ffe6fa13738d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e4c756463c43ede8c6dae0cda0a184f0ec7f9956
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "70154935"
---
# <a name="task-9-configuring-a-reference-data-service"></a>任务 9：配置引用数据服务
  在此任务中，将 DQS 配置为使用 Azure Marketplace 中的引用数据服务。 在下一任务中，将配置**地址验证**域以使用此服务。 在运行时，在清理活动期间，DQS 会将**地址验证**域中的域的值传递到服务进行清理。 有关更多详细信息，请参阅[配置 DQS 以使用引用数据](https://msdn.microsoft.com/library/hh213070.aspx)。  
  
1.  在**DQS 客户端**的主页中，在 "**管理**" 窗格中单击 "**配置**"。  
  
2.  确保 "**引用数据**" 选项卡处于活动状态。  
  
3.  如果需要使用代理服务器连接到 Internet，请在 "**网络设置**" 区域中的 "**代理服务器**" 和 "**端口**" 字段中键入相应的值。  
  
4.  键入 " **DataMarket 帐户 ID** " 字段的**Azure Marketplace 帐户密钥**。  
  
     ![Azure Data Market 引用数据服务帐户](../../2014/tutorials/media/et-configuringareferencedataservice.jpg "Azure Data Market 引用数据服务帐户")  
  
5.  单击文本框旁边的 "**验证**" 按钮以验证帐户 ID。  
  
6.  在消息框中单击 **"确定"** 。  
  
7.  单击页面底部的 "**关闭**" 以切换到 DQS 客户端的主页。  
  
## <a name="next-task"></a>下一个任务  
 [任务 10：配置复合域以使用引用数据服务](../../2014/tutorials/task-10-configuring-composite-domain-to-use-reference-data-service.md)  
  
  
