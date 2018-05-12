---
title: 指定的解决方案部署的配置设置 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f711dc12ed5014dbc397e5a72f97f55350da7d38
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="deployment-script-files---solution-deployment-config-settings"></a>部署脚本文件的解决方案部署配置设置
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署向导读取的分区和角色的部署选项，使用部署脚本从中\<*项目名称*>.configsettings 文件。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]生成时创建此文件[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 使用当前项目的配置设置创建\<*项目名称*>.configsettings 文件。  
  
## <a name="reviewing-the-configuration-settings-for-deployment"></a>检查部署的配置设置  
 以下是中存储的配置设置\<*项目名称*>.configsettings 文件：  
  
-   **数据源连接字符串** 这些是基于 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中指定值的每个数据源的连接字符串。 总是先删除连接字符串中的用户 ID 和密码，然后再在此文件中存储字符串的其余部分。 但是，如果部署向导直接对 Analysis Services 实例进行部署，则可以在向导中添加相应的用户 ID 和密码信息，以便成功地处理部署数据库。 如果部署向导保存了此连接信息，则部署脚本中不存储此信息。  
  
-   **模拟帐户** 此设置指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在每个数据源中运行语句时所用的用户名。 如果未指定模拟帐户， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将使用其登录帐户来运行语句。 如果直接在数据源中向 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 登录帐户授予权限，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中所有数据库的所有数据库管理员均可通过该登录帐户访问数据源。 如果指定用户帐户和密码，则总是先删除此信息，然后再在此文件中存储模拟信息。 但是，如果部署向导直接对 Analysis Services 实例进行部署，则可以在向导中添加相应的用户 ID 和密码信息，以便成功地处理部署数据库。 如果部署向导保存了此模拟信息，则部署脚本中不存储此信息。  
  
-   **键错误日志文件** 此设置为数据库中的每个多维数据集、度量值组、分区和维度指定键错误日志文件的文件名和路径。  
  
-   **存储位置** 此设置为数据库中的每个多维数据集、度量值组和分区指定存储位置。 如果没有为对象提供任何值，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导使用该对象的默认位置。 例如，分区使用度量值组的位置，度量值组使用多维数据集的位置，而多维数据集使用对象在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中的默认位置。 存储位置可以是本地路径，也可以是通用命名约定 (UNC) 路径。  
  
-   **报表服务器** 此设置为数据库的每个多维数据集中定义的每个报表操作指定报表服务器和文件夹位置。  
  
## <a name="modifying-the-configuration-settings-for-deployment"></a>修改部署的配置设置  
 在某些情况下，你可能需要部署[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目使用比存储在不同的配置设置\<*项目名称*>.configsettings 文件。 例如，最好更改一个或多个数据源的连接字符串，或需要为特定的分区或度量值组指定存储位置。  
  
 若要修改的分区和角色中的部署[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目，则必须更改中的此信息\<*项目名称*>.configsettings 文件，如下面的过程中所述。 无法更改项目中的分区和角色设置，因为*\<项目名称 >* **属性页**中的对话框[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]不会显示这些选项。  
  
> [!NOTE]  
>  配置设置可应用于所有对象，也可仅应用于新创建的对象。 仅当要将其他对象部署到以前部署的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中，并且不希望覆盖现有对象时，才将配置设置应用于新创建的对象。 若要指定是否配置设置应用于所有对象，或只是为了新创建的违规时，在中设置此选项\<*项目名称*>.deploymentoptions 文件。 有关详细信息，请参阅[指定分区和角色部署选项](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)。  
  
#### <a name="to-change-configuration-settings-after-the-input-files-have-been-generated"></a>在生成输入文件后更改配置设置  
  
-   以交互方式运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导，然后在 **“配置设置”** 页上，为要部署的对象指定配置设置。  
  
     — 或 —  
  
-   在命令提示符下运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导，并设置向导，使其以应答文件模式运行。 有关应答文件模式的详细信息，请参阅 [Running the Analysis Services Deployment Wizard](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)。  
  
     — 或 —  
  
-   修改\<*项目名称*>.configsettings 文件使用的任何文本编辑器。  
  
## <a name="see-also"></a>另请参阅  
 [指定安装目标](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)   
 [指定分区和角色部署选项](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)   
 [指定处理选项](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
  
