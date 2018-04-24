---
title: 清除版本成员 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: adecce2d-46bb-49ff-8be9-0b31b8dd3cb6
caps.latest.revision: 7
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 26c53b0e050ebdb9682fe8d64dc10f9500d88b46
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="purge-version-members-master-data-services"></a>清除版本成员 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，删除成员仅将其停用或软删除。 数据仍驻留在数据库中。 本主题介绍如何在模型版本中清除（永久删除）所有软删除的成员。  
  
## <a name="prerequisites"></a>必备条件  
 执行此过程。  
  
-   你必须有权访问“版本管理”功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
## <a name="to-purge-soft-deleted-members"></a>清除软删除的成员  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“版本管理”**。  
  
2.  在“管理版本”  页上，选择与要清除的版本对应的模型。 随后显示模型版本的列表。  
  
3.  选择与要清除的版本对应的行。  
  
4.  单击“清除成员” 。  
  
5.  在确认提示中单击“确定”。  
  
## <a name="additional-methods-to-purge-members"></a>清除成员的其他方法  
 清除版本成员会永久删除与所选版本相关的所有实体中的软删除成员。 更精细的替代方法是使用实体基本暂存，仅永久删除实体的特定成员。 此外，具有资源管理器功能权限的实体管理员可能会清除实体资源管理器页中的实体版本。  
  
 有关详细信息，请参阅[叶成员临时表 (Master Data Services)](../master-data-services/leaf-member-staging-table-master-data-services.md)。  
  
  
