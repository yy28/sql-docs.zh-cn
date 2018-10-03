---
title: 任务 9： 配置引用数据服务 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: d0535fce-2bf5-4f6d-b517-ffe6fa13738d
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 23832b226bb9408ab4e5b2fbb50718e1ead710b4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48217287"
---
# <a name="task-9-configuring-a-reference-data-service"></a>任务 9：配置引用数据服务
  在本任务中，您将 DQS 配置为使用 Microsoft Azure 市场上的引用数据服务。 在下一个任务，您将配置**地址验证**域以使用此服务。 在运行时，在清理活动，DQS 将传递的值中的域**地址验证**的域和服务以进行清理。 请参阅[配置 DQS 以使用引用数据](http://msdn.microsoft.com/library/hh213070.aspx)的更多详细信息。  
  
1.  在主页面中的**DQS 客户端**，在**管理**窗格中，单击**配置**。  
  
2.  絋粄**引用数据**选项卡处于活动状态。  
  
3.  在中**网络设置**区域中，键入适当的值中**代理服务器**并**端口**字段如果您需要使用代理服务器连接到 Internet。  
  
4.  类型在**Windows Azure Marketplace 帐户密钥**有关**DataMarket 帐户 ID**字段。  
  
     ![Azure 数据市场引用数据服务帐户](../../2014/tutorials/media/et-configuringareferencedataservice.jpg "Azure 数据市场引用数据服务帐户")  
  
5.  单击**验证**按钮旁边的文本框，以验证帐户 id。  
  
6.  单击**确定**消息框上。  
  
7.  单击**关闭**要切换到 DQS 客户端的主页上的页的底部。  
  
## <a name="next-task"></a>下一个任务  
 [任务 10：配置复合域以使用引用数据服务](../../2014/tutorials/task-10-configuring-composite-domain-to-use-reference-data-service.md)  
  
  
