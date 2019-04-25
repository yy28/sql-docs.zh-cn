---
title: 重叠的模型和成员权限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], effective permissions
- permissions [Master Data Services], model and member overlaps
- members [Master Data Services], effective permissions
ms.assetid: 9fd7a555-43bf-4796-a8b6-1ca63a291216
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: e70b6dab6399026606382396bded3a467a9b639c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62764239"
---
# <a name="overlapping-model-and-member-permissions-master-data-services"></a>重叠的模型和成员权限（主数据服务）
  分配给成员的权限可与分配给模型对象的权限重叠。 出现重叠时，限制性更强的权限将生效。  
  
 如果成员具有不同于其相应模型对象的权限，适用以下规则：  
  
-   **“拒绝”** 覆盖所有其他权限。  
  
-   **只读**重写**更新**。  
  
 下图显示在属性权限不同于成员权限时，哪些权限对单个属性值有效。  
  
 ![mds_conc_security_member_overlap_table](../../2014/master-data-services/media/mds-conc-security-member-overlap-table.gif "mds_conc_security_member_overlap_table")  
  
## <a name="example-1"></a>示例 1  
 ![mds_conc_overlap_model_1](../../2014/master-data-services/media/mds-conc-overlap-model-1.gif "mds_conc_overlap_model_1")  
  
 在 **“模型”** 选项卡上，Product 实体分配有 **“更新”** 权限。 该实体中的所有属性都继承该权限。  
  
 在 **“层次结构成员”** 选项卡上，派生的层次结构中的“山地车”子类别节点分配有 **“更新”** 权限。  
  
 结果：在“资源管理器”中，用户对“山地车”节点中所有成员的所有属性值都具有“更新”权限。 所有其他成员和属性均隐藏。  
  
 ![mds_conc_overlap_model_example_1](../../2014/master-data-services/media/mds-conc-overlap-model-example-1.gif "mds_conc_overlap_model_example_1")  
  
## <a name="example-2"></a>示例 2  
 ![mds_conc_overlap_model_2](../../2014/master-data-services/media/mds-conc-overlap-model-2.gif "mds_conc_overlap_model_2")  
  
 在 **“模型”** 选项卡上，Subcategory 属性分配有 **“更新”** 权限。  
  
 上**层次结构成员**选项卡上，派生层次结构中的山地车子类别节点显式分配**只读**权限。  
  
 结果：在**资源管理器**，用户拥有**只读**所有 Subcategory 属性值的山地车节点中的成员的权限。 所有其他成员和属性均隐藏。  
  
 ![mds_conc_overlap_model_example_2](../../2014/master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## <a name="example-3"></a>示例 3  
 ![mds_conc_overlap_model_3](../../2014/master-data-services/media/mds-conc-overlap-model-3.gif "mds_conc_overlap_model_3")  
  
 上**模型**选项卡上，Subcategory 属性具有**只读**分配权限。  
  
 在 **“层次结构成员”** 选项卡上，派生的层次结构中的“山地车”子类别显式分配有 **“更新”** 权限。  
  
 结果：在**资源管理器**，用户拥有**只读**对属性值的权限。 所有其他成员和属性均隐藏。  
  
 ![mds_conc_overlap_model_example_2](../../2014/master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## <a name="see-also"></a>请参阅  
 [如何确定权限 (Master Data Services)](how-permissions-are-determined-master-data-services.md)   
 [重叠的用户和组权限 &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-user-and-group-permissions-master-data-services.md)  
  
  
