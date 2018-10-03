---
title: 重叠的用户和组权限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- users [Master Data Services], resolving permissions
- permissions [Master Data Services], user and group overlaps
- groups [Master Data Services], resolving permissions
ms.assetid: 31c3cf7d-17d4-4474-b6a7-ffcb9fc45b37
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 0d35c40dd15db4ed9b7cdc7802f3ef306755569d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205417"
---
# <a name="overlapping-user-and-group-permissions-master-data-services"></a>重叠的用户和组权限（主数据服务）
  用户的权限基于：  
  
-   来自组成员身份的权限。  
  
-   显式分配给用户的权限。  
  
 如果用户是多个组的成员，并且这些组有权访问主数据管理器，则适用以下规则：  
  
-   **“拒绝”** 覆盖所有其他权限。  
  
-   **更新**重写**只读**。  
  
 这些规则应用到 **“模型”** 和 **“层次结构成员”** 选项卡。 先为每个选项卡确定权限，再将权限进行组合。 有关详细信息，请参阅[如何确定权限 (Master Data Services)](how-permissions-are-determined-master-data-services.md)  
  
> [!NOTE]  
>  可以在用户界面中查看用户和组的重叠权限的解决方法。 “模型”和“层次结构成员”选项卡都具有下拉列表，可以从中选择“有效”，查看有效权限。  
  
## <a name="example-1"></a>示例 1  
 ![mds_conc_user_group_ex_1](../../2014/master-data-services/media/mds-conc-user-group-ex-1.gif "mds_conc_user_group_ex_1")  
  
 用户同时属于组 1 和组 2。  
  
 用户具有**只读**对 Product 实体的权限。  
  
 组 1 对 Product 实体具有 **“更新”** 权限。  
  
 组 2 具有**只读**对 Product 实体的权限。  
  
 结果：用户对 Product 实体的有效权限是 **“更新”** 。  
  
## <a name="example-2"></a>示例 2  
 ![mds_conc_user_group_ex_2](../../2014/master-data-services/media/mds-conc-user-group-ex-2.gif "mds_conc_user_group_ex_2")  
  
 用户同时属于组 1 和组 2。  
  
 用户具有**只读**对 Product 实体的权限。  
  
 组 1 对 Product 实体具有 **“更新”** 权限。  
  
 组 2 对 Product 实体具有 **“拒绝”** 权限。  
  
 结果：用户对 Product 实体的有效权限是 **“拒绝”** 。  
  
## <a name="example-3"></a>示例 3  
 ![mds_conc_user_group_ex_3](../../2014/master-data-services/media/mds-conc-user-group-ex-3.gif "mds_conc_user_group_ex_3")  
  
 用户同时属于组 1 和组 2。  
  
 用户对层次结构节点中的一组成员具有 **“更新”** 权限。  
  
 组 1 具有**只读**的一组层次结构节点中的成员的权限。  
  
 组 2 具有**只读**的一组层次结构节点中的成员的权限。  
  
 结果：用户对这些成员的有效权限是 **“更新”** 。  
  
## <a name="see-also"></a>请参阅  
 [如何确定权限&#40;Master Data Services&#41;](how-permissions-are-determined-master-data-services.md)   
 [重叠的模型和成员权限 &#40;Master Data Services&#41;](../../2014/master-data-services/overlapping-model-and-member-permissions-master-data-services.md)  
  
  
