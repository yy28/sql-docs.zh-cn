---
title: 提交版本 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- committing versions [Master Data Services]
- versions [Master Data Services], committing
ms.assetid: 6b967a39-b333-4b84-9e5f-4fb07e156826
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 484986c617742967c41160aaf369b3562e72d938
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48085778"
---
# <a name="commit-a-version-master-data-services"></a>提交版本 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，提交某一模型的版本以便防止对该模型的成员及其属性的更改。 已提交的版本无法取消锁定。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行此过程：  
  
-   您必须有权访问 **“版本管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
-   版本的状态必须是 **“已锁定”**。 有关详细信息，请参阅[锁定版本 (Master Data Services)](../../2014/master-data-services/lock-a-version-master-data-services.md)。  
  
-   所有成员必须已经成功验证。  
  
### <a name="to-commit-a-version"></a>提交版本  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“版本管理”**。  
  
2.  在 **“管理版本”** 页上，从菜单栏中，单击 **“验证版本”**。  
  
3.  在 **“验证版本”** 页上，选择要提交的模型和版本。  
  
4.  单击 **“提交”**。  
  
5.  在确认对话框中，单击 **“确定”**。  
  
## <a name="next-steps"></a>后续步骤  
  
-   [创建版本标志&#40;Master Data Services&#41;](../../2014/master-data-services/create-a-version-flag-master-data-services.md)  
  
-   [向版本分配标志&#40;Master Data Services&#41;](../../2014/master-data-services/assign-a-flag-to-a-version-master-data-services.md)  
  
-   [复制版本&#40;Master Data Services&#41;](../../2014/master-data-services/copy-a-version-master-data-services.md)  
  
## <a name="see-also"></a>请参阅  
 [版本&#40;Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)  
  
  
