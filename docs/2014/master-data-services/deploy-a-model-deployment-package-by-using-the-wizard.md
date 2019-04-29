---
title: 使用向导部署模型部署包 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deployment packages [Master Data Services], deploying
- models [Master Data Services], deploying a package
ms.assetid: 4f65dc60-0ff8-46e6-9988-5bc5b9603ad0
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 3b74a2de7cd9479552fdf560a324a93541496eaa
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62925294"
---
# <a name="deploy-a-model-deployment-package-by-using-the-wizard"></a>使用向导部署模型部署包
  使用 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 模型部署向导部署只包含模型对象的包。 如果需要部署包含数据的包，请参阅 [使用 MDSModelDeploy 部署模型部署包](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)。  
  
> [!IMPORTANT]  
>  包只能部署到创建它们的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本中。 这意味着在 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 中创建的包不能部署到 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问目标 **环境中的** “系统管理” [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 功能区域。  
  
-   模型部署包必须存在。 有关详细信息，请参阅 [使用向导创建模型部署包](../../2014/master-data-services/create-a-model-deployment-package-by-using-the-wizard.md)。  
  
-   您必须是部署模型的环境中的管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
### <a name="to-deploy-a-model-deployment-package-of-model-objects-only"></a>仅部署模型对象的模型部署包  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在 **“模型视图”** 页上，从菜单栏中，指向 **“系统”** ，然后单击 **“部署”**。  
  
3.  在 **“模型部署向导”** 上，单击 **“部署”**。  
  
4.  单击 **“浏览”**。  
  
5.  找到部署包（.pkg 文件），然后单击“打开”。  
  
6.  单击“下一步” 。  
  
7.  在加载包后，单击 **“下一步”**。  
  
8.  如果该模型已存在，则可以通过选择 **“更新现有模型”** 更新该模型。 若要创建新模型，请选择 **“创建新模型”** ，并且在单击 **“下一步”** 后，可为该新模型键入名称。  
  
9. 单击 **“完成”** 退出向导。  
  
 **说明：**  
  
-   如果包中的订阅视图现有模型中具有订阅视图同名，视图创建为*modelname.subscriptionviewname*。 如果此名称已使用，则不会创建订阅视图。  
  
-   部署过程具有以下四个步骤：  
  
    1.  创建模型对象。  
  
    2.  创建订阅视图。  
  
    3.  创建业务规则。  
  
    4.  填充主数据。  
  
-   创建一个新的或克隆的模型时，如果该过程在任何步骤期间失败，该模型将被删除。  
  
     在更新模型时，如果该过程在前三个步骤的任意步骤中失败，则该过程将不会继续；但是，已进行的更改将不会回滚。 如果该过程在步骤 4 中失败，则会更新可更新的成员。  
  
## <a name="next-steps"></a>后续步骤  
 在模型部署包中不包括用户定义元数据、文件属性以及用户和组权限。 在您部署模型后，必须手动更新这些内容。 有关详细信息，请参阅：  
  
-   [添加元数据&#40;Master Data Services&#41;](../../2014/master-data-services/add-metadata-master-data-services.md)  
  
-   [分配模型对象权限 (Master Data Services)](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>请参阅  
 [部署模型 (Master Data Services)](../../2014/master-data-services/deploying-models-master-data-services.md)  
  
  
