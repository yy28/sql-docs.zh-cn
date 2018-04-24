---
title: 使用向导部署模型部署包 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
helpviewer_keywords:
- deployment packages [Master Data Services], deploying
- models [Master Data Services], deploying a package
ms.assetid: 4f65dc60-0ff8-46e6-9988-5bc5b9603ad0
caps.latest.revision: 16
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d661b7d42d08884d7908f0de36bc3efc1956998c
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="deploy-a-model-deployment-package-by-using-the-wizard"></a>使用向导部署模型部署包

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  使用 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 模型部署向导部署只包含模型对象的包。 如果需要部署包含数据的包，请参阅 [使用 MDSModelDeploy 部署模型部署包](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)。  
  
> [!IMPORTANT]  
>  包只能部署到创建它们的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本中。 这意味着在 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中创建的包不能部署到 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]。  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-   您必须有权访问目标 **环境中的** “系统管理” [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 功能区域。  
  
-   模型部署包必须存在。 有关详细信息，请参阅 [使用向导创建模型部署包](../master-data-services/create-a-model-deployment-package-by-using-the-wizard.md)。  
  
-   您必须是部署模型的环境中的管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
### <a name="to-deploy-a-model-deployment-package-of-model-objects-only"></a>仅部署模型对象的模型部署包  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在 **“模型视图”** 页上，从菜单栏中，指向 **“系统”** ，然后单击 **“部署”**。  
  
3.  在 **“模型部署向导”**上，单击 **“部署”**。  
  
4.  单击 **“浏览”**。  
  
5.  找到部署包（.pkg 文件），然后单击“打开”。  
  
6.  单击“下一步” 。  
  
7.  在加载包后，单击 **“下一步”**。  
  
8.  如果该模型已存在，则可以通过选择 **“更新现有模型”**更新该模型。 若要创建新模型，请选择 **“创建新模型”** ，并且在单击 **“下一步”** 后，可为该新模型键入名称。  
  
9. 单击 **“完成”** 退出向导。  
  
 **说明：**  
  
-   如果包中的订阅视图与现有模型中的订阅视图同名，则显示此警告： **Deployer 订阅视图已重命名**。 另外，视图已创建为 *modelname.subscriptionviewname*。 如果此名称已使用，则不会创建订阅视图。  
  
-   部署过程具有以下四个步骤：  
  
    1.  创建模型对象。  
  
    2.  创建订阅视图。  
  
    3.  创建业务规则。  
  
-   创建一个新的或克隆的模型时，如果该过程在任何步骤期间失败，该模型将被删除。  
  
     在更新模型时，如果该过程在前三个步骤的任意步骤中失败，则该过程将不会继续；但是，已进行的更改将不会回滚。  
  
## <a name="next-steps"></a>Next Steps  
 模型部署包中不包括文件属性以及用户和组权限。 在您部署模型后，必须手动更新这些内容。 有关详细信息，请参阅：  
  
-   [分配模型对象权限 (Master Data Services)](../master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>另请参阅  
 [部署模型 (Master Data Services)](../master-data-services/deploying-models-master-data-services.md)  
  
  
