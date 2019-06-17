---
title: 锁定版本 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- versions [Master Data Services], locking
- locking versions [Master Data Services]
ms.assetid: 7bb62a84-12d8-4b29-9b6e-6aa25410618e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e38a4c75ad6cf8c65d7120e0eb98163f7ee0fccc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482874"
---
# <a name="lock-a-version-master-data-services"></a>锁定版本 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，锁定某一模型的版本以便防止对该模型的成员及其属性的更改。  
  
> [!NOTE]  
>  在锁定某一版本后，模型管理员可以继续添加、编辑和删除成员。 对模型具有权限的其他用户只能查看成员。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“版本管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
-   版本的状态必须是 **“打开”** 。  
  
### <a name="to-lock-a-version"></a>锁定版本  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“版本管理”** 。  
  
2.  在 **“管理版本”** 页上，选择要锁定的版本对应的行。  
  
3.  单击 **“锁定”** 。  
  
4.  在确认对话框中，单击 **“确定”** 。  
  
## <a name="next-steps"></a>后续步骤  
  
-   [针对业务规则验证版本 (Master Data Services)](../../2014/master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   [提交版本 (Master Data Services)](../../2014/master-data-services/commit-a-version-master-data-services.md)  
  
## <a name="see-also"></a>请参阅  
 [版本 (Master Data Services)](../../2014/master-data-services/versions-master-data-services.md)   
 [取消锁定版本 (Master Data Services)](../../2014/master-data-services/unlock-a-version-master-data-services.md)  
  
  
