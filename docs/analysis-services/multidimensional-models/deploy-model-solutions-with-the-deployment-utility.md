---
title: 使用部署实用工具部署模型解决方案 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 76d1a3e3cfff777f610bb00f52644af3903ac615
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37975158"
---
# <a name="deploy-model-solutions-with-the-deployment-utility"></a>使用部署实用工具部署模型解决方案
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  可以使用 **Microsoft.AnalysisServices.Deployment** 实用工具在命令提示符下启动 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署引擎。 此实用工具使用的输入文件，是在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中生成 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]项目时生成的 XML 输出文件。 可以轻松修改输入文件，以自定义 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的部署。 随后，可以立即运行生成的部署脚本，也可以保留此脚本供以后部署。  
  
> [!NOTE]
> [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]部署向导实用程序随[SQL Server 管理 Studio](../../ssms/download-sql-server-management-studio-ssms.md) (SSMS)。 请确保使用最新版本。 默认情况下，部署向导的最新版本安装到 C:\Program Files (x86) \Microsoft SQL Server\140\Tools\Binn\ManagementStudio。 

## <a name="syntax"></a>语法  
  
```  
  
Microsoft.AnalysisServices.Deployment [ASdatabasefile]   
    {[/s[:logfile]] | [/a] | [[/o[:output_script_file]] [/d]]}  
```  
  
##  <a name="Arguments"></a> 参数  
 *ASdatabasefile*  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署脚本 (.asdatabase) 文件所在文件夹的完整路径。 当您在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中部署一个项目时生成此文件。 该文件位于项目的 bin 文件夹中。 .asdatabase 文件包含要部署的对象定义的位置。 如果不指定路径，则使用当前文件夹。  
  
 **/s**  
 以静默模式运行此实用工具，不显示任何对话框。 有关各种模式的详细信息，请参阅本主题后面的 [模式](#Modes)部分。  
  
 *logfile*  
 日志文件的完整路径和文件名。 将在指定的日志文件中记录跟踪事件。 如果日志文件已经存在，则其内容将被替换。  
  
 **/a**  
 在应答模式中运行此实用工具。 执行此实用工具向导部分产生的所有响应应写回输入文件，但不会实际更改部署目标。  
  
 **/o**  
 以输出模式运行此实用工具。 此模式下将不进行部署，但是通常会将发送到部署目标的 XML for Analysis (XMLA) 脚本转而保存到指定的输出脚本文件。 如果未指定 *output_script_file* ，则该实用工具将尝试使用在部署选项 (.deploymentoptions) 输入文件中所指定的输出脚本文件。 如果部署选项输入文件中未指定输出脚本文件，则将出现错误。  
  
 有关各种模式的详细信息，请参阅本主题后面的 [模式](#Modes)部分。  
  
 *output_script_file*  
 输出脚本文件的完整路径和文件名。  
  
 **/d**  
 如果使用 **/o** 参数，则指定此实用工具不应连接到目标实例。 由于未与部署目标连接，因此仅根据从输入文件检索到的信息生成输出脚本。  
  
> [!NOTE]  
>  **/d** 参数只在输出模式下使用。 在应答模式或静默模式下，将忽略此参数。 有关各种模式的详细信息，请参阅本主题后面的 [模式](#Modes)部分。  
  
## <a name="remarks"></a>Remarks  
 **Microsoft.AnalysisServices.Deployment** 实用工具将使用一组文件，这些文件可以提供对象定义、部署目标、部署选项和配置设置。同时，该实用工具将使用指定的部署选项和配置设置，尝试将对象定义部署到指定的部署目标。 如果在应答文件中或在输出模式下调用此实用工具，此工具可提供一个用户界面。 有关如何使用为此实用工具提供的用户界面创建应答文件的详细信息，请参阅 [使用部署向导部署模型解决方案](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)。  
  
 此实用工具位于 \Program files (x86) \Microsoft SQL Server\140\Binn\ManagementStudio 文件夹中。  
  
##  <a name="Modes"></a> 模式  
 此实用工具可以在下表列出的模式下运行。  
  
|“模式”|Description|  
|----------|-----------------|  
|静默模式|不会显示任何用户界面，部署所需要的全部信息均由输入文件提供。 在静默模式下，此实用工具不显示进度。 但可使用可选的日志文件捕获进度和错误信息供以后查看。|  
|应答模式|显示部署向导用户界面，并将用户响应保存到指定的输入文件供以后部署。 不会在应答模式下进行部署。 应答模式的唯一用途是捕获用户响应|  
|输出模式|不会显示任何用户界面，部署所需要的全部信息均由输入文件提供。<br /><br /> 但是，与静默模式不同，此实用工具的输出被写入输出脚本文件，而不是发送到输入文件中指示的部署目标。 除非指定了 **/d** 参数，否则此实用工具将与每个部署目标连接，以便在生成输出脚本文件时比较元数据。|  
  
 [返回到参数](#Arguments)  
  
## <a name="examples"></a>示例  
 以下示例演示了如何在静默模式下部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目，并记录进度和错误消息供以后查看：  
  
 `Microsoft.AnalysisServices.Deployment.exe`  
  
 `<drive>:\My Documents\Visual Studio 2010\Projects\AdventureWorksProject\Project1\bin`  
  
 `/s: C:\ My Documents\Visual Studio 2010\Projects\AdventureWorksProject\Project1\bin\deployment.log`  
  
## <a name="see-also"></a>请参阅  
 [命令提示实用工具参考（数据库引擎）](../../tools/command-prompt-utility-reference-database-engine.md)  
  
  
