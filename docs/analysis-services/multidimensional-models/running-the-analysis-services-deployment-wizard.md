---
title: "运行 Analysis Services 部署向导 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Analysis Services Deployment Wizard, running
ms.assetid: 3a38d489-4625-4878-bd18-c6f903be33df
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 2d6a1102ed83493e25e3e73a0b77d035c2e299d9
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="running-the-analysis-services-deployment-wizard"></a>运行 Analysis Services 部署向导
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]当你使用[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署向导部署[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目中，你可以通过以下方式运行该向导：  
  
-   **以交互方式**交互式运行时，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署向导生成部署脚本基于输入文件中，由用户输入以交互方式修改。 此向导将任何用户的更改仅应用于部署脚本。 向导不会更改输入文件。 有关输入文件的详细信息，请参阅 [了解用于创建部署脚本的输入文件](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)。  
  
-   **从命令提示符**在命令提示符处，运行时[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署向导生成部署脚本基于用于运行该向导的开关。 该向导可以指导进行下面的任何一项操作：提示用户输入并基于输入更改输入文件；按原样使用输入文件以静默、无人参与模式运行部署；或创建一个以后可能使用的部署脚本。  
  
## <a name="running-the-analysis-services-deployment-wizard-interactively"></a>交互式运行 Analysis Services 部署向导  
 进行交互式运行时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导读取输入文件中的值并向您显示该信息。 可以更改这些输入值 - 例如部署目标、配置设置、部署选项和连接字符串密码 - 或原样保留它们。 如果更改任何输入的值，则向导将生成部署脚本时使用这些更改。 但是，向导不会更改输入文件中的任何值。  
  
> [!NOTE]  
>  如果使 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导更改输入值，那么可以在命令提示符处运行向导并将向导设置为以应答文件模式运行。  
  
 查看输入的值并进行任何需要的更改后，向导将生成部署脚本。 可以立即在目标服务器上运行该部署脚本或者保存该脚本以备将来使用。  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-interactively"></a>交互式运行 Analysis Services 部署向导  
  
-   单击 **“开始”**，依次指向 **“所有程序”**、 **“Microsoft SQL Server”**和 **“Analysis Services”**，然后单击 **“部署向导”**。  
  
     — 或 —  
  
-   在**项目**文件夹[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]项目中，双击\<项目名称 >.asdatabase 文件。
    > [!NOTE]  
    >  如果未找到 .asdatabase 文件，则请尝试使用“搜索”功能以 *.asdatabase 形式进行搜索。 或者，你可能需要生成 SSDT 中的项目。  
  
## <a name="running-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>在命令提示符下运行 Analysis Services 部署向导  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导也可以在命令提示符下运行。 在命令提示符下运行该向导时，应提供 .asdatabase 文件的完整路径，并使用下列模式之一运行该向导：  
  
 **应答文件模式**  
 使用应答文件模式，在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中生成 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]项目时，向导允许你交互式更改最初生成的输入文件。 向导在生成部署脚本之前保存这些更改过的输入的文件。 这些更改过的输入文件便成为向导下次运行时的新起点。  
  
 若要在应答文件模式运行向导，使用**/a**切换。  
  
 **静默模式**  
 使用静默模式，向导基于输入文件中的信息以静默、无人参与的模式运行部署。  
  
 若要在静默模式下运行该向导，使用**/s**切换。 如果以静默模式运行向导，则消息将输出至控制台或日志文件（如果有）。  
  
 **输出模式**  
 在输出模式下，向导将生成基于输入文件的更高版本执行的部署脚本。  
  
 若要在输出模式中运行该向导，使用**/o**切换，并提供输出文件的名称。  
  
 有关此类命令行开关的详细信息，请参阅 [使用部署实用工具部署模型解决方案](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)。  
  
 下面的过程说明了如何在命令提示符下运行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导。  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>在命令提示符下运行 Analysis Services 部署向导  
  
1.  打开命令提示符，然后导航到 C:\Program Files (x86)\Microsoft SQL Server\120\Tools\Binn\ManagementStudio。  
  
2.  键入 **Microsoft.AnalysisServices.Deployment.exe** ，后跟与要使用的向导运行模式相对应的开关。  
  
## <a name="see-also"></a>另请参阅  
 [了解 Analysis Services 部署脚本](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)   
 [使用部署向导部署模型解决方案](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)  
  
  
