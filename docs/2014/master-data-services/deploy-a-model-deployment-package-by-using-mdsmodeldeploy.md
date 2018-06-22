---
title: 使用 MDSModelDeploy 部署模型部署包 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fb2a4df4-5e0d-4b34-818f-383dbde1b15c
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e99859dcdfcc2061622e955399b6d7bdac8bcbf4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015713"
---
# <a name="deploy-a-model-deployment-package-by-using-mdsmodeldeploy"></a>使用 MDSModelDeploy 部署模型部署包
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，使用 MDSModelDeploy 工具来部署包含以下任一信息的包：  
  
-   仅模型对象。  
  
-   模型对象和数据。  
  
 如果需要部署仅包含模型对象的包，可改为在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序中使用模型部署向导。 有关详细信息，请参阅 [Deploy a Model Deployment Package by Using the Wizard](../../2014/master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)。  
  
> [!IMPORTANT]  
>  包只能部署到创建它们的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本中。 这意味着在 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 中创建的包不能部署到 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 或更高版本。  
  
## <a name="prerequisites"></a>必要條件  
 若要执行此过程：  
  
-   您必须有权访问目标 **环境中的** “系统管理” [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 功能区域。  
  
-   模型部署包必须存在。 有关详细信息，请参阅  [Create a Model Deployment Package by Using MDSModelDeploy](../../2014/master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)。  
  
-   您必须是部署模型的环境中的管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](administrators-master-data-services.md)。  
  
-   如果您正在更新包含数据的模型，则不能 **“锁定”** 或 **“提交”** 正在部署到的版本。  
  
### <a name="to-deploy-a-model-deployment-package"></a>部署模型部署包  
  
1.  确定您是在部署一个新模型、部署模型的一个克隆副本，还是在更新先前克隆的模型。 有关详细信息，请参阅[模型部署选项 (Master Data Services)](../../2014/master-data-services/model-deployment-options-master-data-services.md)  
  
2.  打开命令提示符，然后导航到 MDSModelDeploy.exe。  
  
    -   如果 MDS 安装在默认位置，该工具位于*驱动器*: files\microsoft SQL Server\120\Master 数据 Services\Configuration\MDSModelDeploy.exe  
  
    -   如果 MDS 未安装在默认位置，请在本地计算机上搜索 MDSModelDeploy.exe。  
  
3.  可选。 查看选项和帮助。  
  
    -   若要显示所有可用选项，请键入 `MDSModelDeploy` ，然后按 Enter 键。  
  
    -   若要显示某个选项的帮助，请键入以下命令，其中 OptionName 是该选项的名称：`MDSModelDeploy help OptionName`。  
  
4.  可选。 如果您有多个 Web 应用程序，通过键入下面的命令并按 Enter 键，确定您要部署到的服务的名称：  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     随即返回一个值列表，例如 `MDS1, Default Web Site, MDS`。 需要此列表中的第一个值（在此例中为 `MDS1`）来部署模型。  
  
5.  根据您是在创建模型部署、克隆模型还是更新模型，在命令提示符处，键入以下命令并按 Enter 键。  
  
    -   创建新模型：  
  
        ```  
        MDSModelDeploy deploynew –package PackageName -model ModelName -service ServiceName  
        ```  
  
    -   创建模型的克隆：  
  
        ```  
        MDSModelDeploy deployclone –package PackageName  
        ```  
  
    -   更新现有模型及其数据：  
  
        ```  
        MDSModelDeploy deployupdate –package PackageName –version VersionName  
        ```  
  
    > [!IMPORTANT]  
    >  如果使用 MDSModelDeploy 工具更新现有模型及其数据，并且该包不包含目标模型中存在的实体、属性或成员，则 MDSModelDeploy 不会从模型中删除此实体、属性或成员。  
  
     其中，PackageName 是包文件 (.pkg) 的名称，ModelName 是新模型的名称，VersionName 是版本的名称，ServiceName 是上一步中返回的服务的名称。 确保模型名称和版本名称完全匹配区分大小写的名称。  
  
6.  成功部署包后，将显示一条消息“MDSModelDeploy 操作已成功完成”。  
  
 **说明：**  
  
-   如果包中的订阅视图具有现有模型中的订阅视图同名，作为创建视图*modelname.subscriptionviewname*。 如果此名称已使用，则不会创建订阅视图。  
  
-   部署过程具有以下四个步骤：  
  
    1.  创建模型对象。  
  
    2.  创建业务规则。  
  
    3.  创建订阅视图。  
  
    4.  填充主数据。  
  
-   创建一个新的或克隆的模型时，如果该过程在任何步骤期间失败，该模型将被删除。  
  
     在更新某一模型时，如果该过程在前三个步骤中失败，则该过程将不会继续；但是，已进行的更改将不会回滚。 如果该过程在步骤 4 中失败，则会更新可更新的成员。  
  
## <a name="next-steps"></a>后续步骤  
 在模型部署包中不包括用户定义元数据、文件属性以及用户和组权限。 在您部署模型后，必须手动更新这些内容。 有关详细信息，请参阅：  
  
-   [添加元数据&#40;Master Data Services&#41;](../../2014/master-data-services/add-metadata-master-data-services.md)  
  
-   [分配模型对象权限&#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>请参阅  
 [部署模型&#40;Master Data Services&#41;](../../2014/master-data-services/deploying-models-master-data-services.md)  
  
  