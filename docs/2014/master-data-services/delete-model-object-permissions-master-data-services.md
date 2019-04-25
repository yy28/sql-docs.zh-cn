---
title: 删除模型对象权限 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting model object permissions [Master Data Services]
- permissions [Master Data Services], deleting model object permissions
- models [Master Data Services], deleting object permissions
ms.assetid: 859c5952-f600-4940-8064-1afd13f7f6dc
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 4e9dfc21fe4f408362c4e8d32f39533c9d271136
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62765612"
---
# <a name="delete-model-object-permissions-master-data-services"></a>删除模型对象权限 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，删除模型对象权限可以删除已进行的任何分配。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“用户和组权限”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
### <a name="to-delete-model-object-permissions"></a>删除模型对象权限  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“用户和组权限”**。  
  
2.  在 **“用户”** 或 **“组”** 页上，选择要编辑的用户或组所对应的行。  
  
3.  单击 **“编辑所选用户”**。  
  
4.  单击 **“模型”** 选项卡。  
  
5.  也可以从 **“模型”** 列表中选择某一模型。  
  
6.  在中**模型权限摘要**窗格中，选择你想要删除的权限的行。  
  
7.  单击**删除所选的权限**。  
  
    > [!NOTE]  
    >  如果权限继承自一个组，则不能从用户删除该权限。 而是必须从该组删除该权限。  
  
## <a name="see-also"></a>请参阅  
 [模型对象权限 (Master Data Services)](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [分配模型对象权限 (Master Data Services)](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)  
  
  
