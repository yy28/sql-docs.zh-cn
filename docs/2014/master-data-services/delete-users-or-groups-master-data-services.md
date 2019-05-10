---
title: 删除用户或组 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting groups [Master Data Services]
- groups [Master Data Services], deleting
- users [Master Data Services], deleting
- deleting users [Master Data Services]
ms.assetid: 0bbf9d2c-b826-48bb-8aa9-9905db6e717f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0114aa3ca6f6744303c3053003a622185d33f547
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65479903"
---
# <a name="delete-users-or-groups-master-data-services"></a>删除用户或组 (Master Data Services)
  在您不再希望用户或组访问 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]时删除它们。  
  
 在删除用户和组时请注意以下行为：  
  
-   如果您删除的用户是有权访问 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]的组的成员，则在您从 Active Directory 或本地组中删除该用户之前，该用户仍能够访问 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 。  
  
-   如果您删除某一组，则该组中有权访问 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 的所有用户都将在您删除它们之前显示在 **“用户”** 列表中。  
  
-   对安全性所做的更改在 20 分钟之内不会传播到 MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“用户和组权限”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
### <a name="to-delete-users-or-groups"></a>删除用户或组  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“用户和组权限”**。  
  
2.  若要删除某一用户，请保持在 **“用户”** 页上。 若要删除某一组，请从菜单栏中单击“管理组”。  
  
3.  在网格中，选择你要删除的用户或组所对应的行。  
  
4.  单击 **“删除所选用户”** 或 **“删除所选组”**。  
  
5.  在确认对话框中，单击 **“确定”**。  
  
## <a name="see-also"></a>请参阅  
 [安全性 (Master Data Services)](../../2014/master-data-services/security-master-data-services.md)  
  
  
