---
title: 创建订阅视图（主数据服务） |微软文档
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
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c4a2f747192b1cddefeac256d4470a2b345305de
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "65479939"
---
# <a name="create-a-subscription-view-master-data-services"></a>创建订阅视图 (Master Data Services)
  如果要在[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]数据库中创建数据视图，以便订阅系统使用，请创建订阅视图。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“集成管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员&#40;主数据服务&#41;](administrators-master-data-services.md)。  
  
### <a name="to-create-a-subscription-view"></a>创建订阅视图  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“集成管理”**。  
  
2.  在菜单栏中，单击 **“创建视图”**。  
  
3.  在 **"订阅视图"** 页上，单击"**添加订阅"视图**。  
  
4.  在 **"创建订阅视图"** 窗格中，在 **"订阅视图"名称**框中键入视图的名称。  
  
5.  从 **“模型”** 列表中，选择某一模型。  
  
6.  选择 **"版本**"或 **"版本标志"** 选项，然后从相应的列表中选择。  
  
    > [!TIP]  
    >  基于版本标志创建订阅视图。 当锁定版本时，可以将该标志重新分配给打开的版本，而无需更新订阅视图。  
  
7.  选择 **"实体**"或"**派生"层次结构**选项，然后从相应的列表中选择。  
  
8.  从 **“格式”** 列表中，选择订阅视图格式。  
  
9. 如果您从 **“格式”** 列表中选择 **“显式级别”** 或 **“派生级别”** ，则键入要包括在视图中的层次结构中的级别数。  
  
10. 单击“ **保存**”。  
  
## <a name="see-also"></a>另请参阅  
 [导出数据&#40;主数据服务&#41;](overview-exporting-data-master-data-services.md)   
 [删除订阅视图&#40;主数据服务&#41;](delete-a-subscription-view-master-data-services.md)   
 [创建版本标志 (Master Data Services)](create-a-version-flag-master-data-services.md)  
  
  
