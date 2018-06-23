---
title: 创建订阅视图 (Master Data Services) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- subscription views [Master Data Services], creating
- creating subscription views [Master Data Services]
ms.assetid: a5e28961-af16-414a-9845-d2e06aac5214
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 0b79bd1e50871fb921a3ce2b3fe9e43ab0995a9e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127111"
---
# <a name="create-a-subscription-view-master-data-services"></a>创建订阅视图 (Master Data Services)
  你想要创建的视图中的数据时创建订阅视图[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]供订阅系统使用的数据库。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行此过程：  
  
-   您必须有权访问 **“集成管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
### <a name="to-create-a-subscription-view"></a>若要创建订阅视图  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“集成管理”**。  
  
2.  在菜单栏中，单击 **“创建视图”**。  
  
3.  上**订阅视图**页上，单击**添加订阅视图**。  
  
4.  在**创建订阅视图**窗格中，请在**订阅视图名称**框中，键入视图的名称。  
  
5.  从 **“模型”** 列表中，选择某一模型。  
  
6.  选择**版本**或**版本标志**选项，然后再选中从相应的列表。  
  
    > [!TIP]  
    >  基于版本标志创建订阅视图。 当锁定版本时，可以将该标志重新分配给打开的版本，而无需更新订阅视图。  
  
7.  选择**实体**或**派生层次结构**选项，然后再选中从相应的列表。  
  
8.  从 **“格式”** 列表中，选择订阅视图格式。  
  
9. 如果您从 **“格式”** 列表中选择 **“显式级别”** 或 **“派生级别”** ，则键入要包括在视图中的层次结构中的级别数。  
  
10. 单击 **“保存”**。  
  
## <a name="see-also"></a>请参阅  
 [导出数据&#40;Master Data Services&#41;](overview-exporting-data-master-data-services.md)   
 [删除订阅视图 &#40;Master Data Services&#41; ](delete-a-subscription-view-master-data-services.md)   
 [创建版本标志&#40;Master Data Services&#41;](create-a-version-flag-master-data-services.md)  
  
  