---
title: "合并冲突 (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 797219ad-5109-4666-94d3-dd1d59440a33
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 18254780cba8b4d0b61116d4f148f3feb656c30a
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2018
---
# <a name="merge-conflicts-master-data-services"></a>合并冲突 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，如果你尝试发布的数据已被另一个用户更改，则发布将失败并显示冲突错误。 若要解决此错误，可以执行合并冲突，然后重新发布更改。  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-    您必须有权访问“资源管理器”功能区域。  
  
-   对于你要更新的实体的叶模型对象，你必须至少具有更新权限。  
  
### <a name="to-merge-conflicts"></a>合并冲突  
  
1.  在  “资源管理器”页上，更新成员属性。  
  
2.  如果同一成员属性已被另一个用户更改，将会出现“合并冲突”  对话框。  
  
3.  在“合并冲突”  对话框中，可以执行以下任一操作：  
  
    -   选择“最新”  ，然后单击“应用”  以撤消挂起的更改并从服务器重新加载最新版本。  
  
    -   选择“原始”  ，然后单击“应用”  以在工作表中应用原始版本。  
  
    -   选择“你的变更”  ，然后单击“应用  以保留现有的本地更改。  
  
4.  单击“应用” 后，可以进行其他更改，并再次发布。 或者，可以单击“取消”  以取消更新并从服务器重新加载最新的版本。  
  
## <a name="see-also"></a>另请参阅  
 [成员 (Master Data Services)](../master-data-services/members-master-data-services.md)  
  
  
