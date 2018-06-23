---
title: 任务 9： 配置引用数据服务 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d0535fce-2bf5-4f6d-b517-ffe6fa13738d
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5a08d3848ddaf65b9e10b654f55e8a0a4d9be690
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36139127"
---
# <a name="task-9-configuring-a-reference-data-service"></a>任务 9：配置引用数据服务
  在本任务中，您将 DQS 配置为使用 Microsoft Azure 市场上的引用数据服务。 在下一步的任务中，你将配置**地址验证**域，以便使用此服务。 在运行时，在清理活动，DQS 将值传递的域的**地址验证**到的服务进行清理的域。 请参阅[Configure DQS to Use Reference Data](http://msdn.microsoft.com/library/hh213070.aspx)有关详细信息。  
  
1.  在主页面中的**DQS 客户端**中**管理**窗格中，单击**配置**。  
  
2.  确保**引用数据**选项卡处于活动状态。  
  
3.  在**网络设置**区域中，键入适当的值中**代理服务器**和**端口**字段如果你需要使用代理服务器连接到 Internet。  
  
4.  类型你**Windows Azure Marketplace 帐户密钥**为**DataMarket 帐户 ID**字段。  
  
     ![Azure 数据市场引用数据服务帐户](../../2014/tutorials/media/et-configuringareferencedataservice.jpg "Azure 数据市场引用数据服务帐户")  
  
5.  单击**验证**按钮旁边的文本框，以验证帐户 id。  
  
6.  单击**确定**消息框上。  
  
7.  单击**关闭**页后，可以切换到 DQS 客户端的主页面底部。  
  
## <a name="next-task"></a>下一个任务  
 [任务 10：配置复合域以使用引用数据服务](../../2014/tutorials/task-10-configuring-composite-domain-to-use-reference-data-service.md)  
  
  