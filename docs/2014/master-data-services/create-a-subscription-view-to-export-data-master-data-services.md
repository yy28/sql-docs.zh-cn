---
title: 创建订阅视图 (Master Data Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- subscription views [Master Data Services], creating
- creating subscription views [Master Data Services]
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: cf14f942857361256febd4329a116c2d349659a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62765812"
---
# <a name="create-a-subscription-view-master-data-services"></a>创建订阅视图 (Master Data Services)
  如果想要创建的视图中的数据创建订阅视图[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]供订阅系统使用的数据库。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“集成管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
### <a name="to-create-a-subscription-view"></a>若要创建订阅视图  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“集成管理”**。  
  
2.  在菜单栏中，单击 **“创建视图”**。  
  
3.  上**订阅视图**页上，单击**添加订阅视图**。  
  
4.  在中**创建订阅视图**窗格中，在**订阅视图名称**框中，键入视图的名称。  
  
5.  从 **“模型”** 列表中，选择某一模型。  
  
6.  选择任一**版本**或**版本标志**选项，然后从相应的列表中选择。  
  
    > [!TIP]  
    >  基于版本标志创建订阅视图。 当锁定版本时，可以将该标志重新分配给打开的版本，而无需更新订阅视图。  
  
7.  选择任一**实体**或**派生层次结构**选项，然后从相应的列表中选择。  
  
8.  从 **“格式”** 列表中，选择订阅视图格式。  
  
9. 如果您从 **“格式”** 列表中选择 **“显式级别”** 或 **“派生级别”** ，则键入要包括在视图中的层次结构中的级别数。  
  
10. 单击“保存” 。  
  
## <a name="see-also"></a>请参阅  
 [将数据导出&#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)   
 [删除订阅视图 &#40;Master Data Services&#41; ](delete-a-subscription-view-master-data-services.md)   
 [创建版本标志 (Master Data Services)](create-a-version-flag-master-data-services.md)  
  
  
