---
title: 创建叶成员 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- leaf members [Master Data Services], creating
- creating leaf members [Master Data Services]
- members [Master Data Services], creating leaf members
ms.assetid: 0499d3b3-d508-4d43-a740-19cf53ade9f1
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 43108a02bb4eace9fda31fd8cdd1c75cefaadcc1
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65487480"
---
# <a name="create-a-leaf-member-master-data-services"></a>创建叶成员 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，如果你想将主数据添加到系统中，请创建叶成员。 如果你想批量添加数据，请改用临时表。 有关详细信息，请参阅[导入表中数据 (Master Data Services)](../master-data-services/import-data-from-tables-master-data-services.md)  
  
 你也可以使用 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 导入数据。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-    您必须有权访问“资源管理器”功能区域。  
  
-   对于要向其中添加成员的实体，你必须至少具有对叶模型对象的“创建”  或“更新”  权限。 拥有“创建”权限后，你可以创建成员，并仅编辑 Code 属性。 拥有“更新”权限后，你可以更新其他属性。  
  
     有关详细信息，请参阅[安全性 (Master Data Services)](../master-data-services/security-master-data-services.md)  
  
### <a name="to-create-a-leaf-member"></a>创建叶成员  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 在  主页上，从“模型”列表中，选择模型。  
  
2.  如果您是用户，则从 **“版本”** 列表中选择某一打开的版本。 如果您是管理员，则从 **“版本”** 列表中选择某一状态为打开或已锁定的版本。  
  
3.  单击 **“资源管理器”**。  
  
4.  从菜单栏中，指向 **“实体”** ，然后单击您要将成员添加到的实体的名称。  
  
5.  单击 **“添加成员”**。  
  
6.  在 **“详细信息”** 窗格中，填写字段。  
  
     如果属性基于域且筛选器已应用于该属性，那么筛选器父属性会约束属性值的列表。  
  
     若要详细了解筛选器父属性和基于域的属性，请参阅[创建基于域的属性 (Master Data Services)](../master-data-services/create-a-domain-based-attribute-master-data-services.md)。  
  
7.  可选。  在“批注”框中，键入有关添加成员原因的注释。 有权访问成员的所有用户都可以查看批注。  
  
8.  单击“确定” 。  
  
## <a name="see-also"></a>请参阅  
 [创建合并成员 (Master Data Services)](../master-data-services/create-a-consolidated-member-master-data-services.md)   
 [成员 (Master Data Services)](../master-data-services/members-master-data-services.md)  
  
  
