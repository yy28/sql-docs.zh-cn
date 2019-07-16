---
title: 生成 Analysis Services 项目 (SSDT) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b00fecf6712d8ab1d4ba8b810485af6d432479ac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209129"
---
# <a name="build-analysis-services-projects-ssdt"></a>生成 Analysis Services 项目 (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  可以在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中生成 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目，就像在 Visual Studio 中生成任何编程项目一样。 生成项目时，会在输出目录中创建一组 XML 文件。 这些 XML 文件使用 Analysis Services 脚本语言 (ASSL)，此脚本语言是 XML 方言，可供包括 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 和 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 在内的客户端应用程序用来与 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例进行通信以创建或修改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象。 这些 XML 文件用于将 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象定义部署到指定的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。  
  
## <a name="building-a-project"></a>生成项目  
 生成 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目时， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 将在输出文件夹中生成一组完整的 XML 文件，其中包含生成此项目中所有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库对象所需的所有必要的 ASSL 命令。 如果项目先前已生成并针对活动配置指定了增量部署，则 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 还将生成一个 XML 文件，其中包含对已部署对象执行增量更新所用的 ASSL 命令。 此 XML 文件将写入项目的 ..\obj\\<active configuration\> 文件夹。 当部署和处理非常庞大的项目或数据库时，使用增量生成可以节省时间。  
  
> [!NOTE]  
>  您可以使用“全部重新生成”命令忽略增量部署设置。  
  
 生成 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目时，会对项目中的对象定义进行验证， 验证对象包括所有被引用的程序集。 生成的错误将显示在“任务列表”窗口以及分析管理对象 (AMO) 错误文本中。 您可以单击一个错误，打开修正此错误所需的设计器。  
  
 成功验证并不保证在部署或部署后成功处理的过程中，可以在目标服务器上创建对象。 下列问题可能会阻止部署或部署后处理的成功进行：  
  
-   无法对服务器执行安全检查，因此锁可能会阻止部署。  
  
-   无法验证服务器上的物理位置。  
  
-   无法根据目标服务器上的实际数据源检查数据源视图的详细信息。  
  
 如果验证成功，则 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 会生成 XML 文件。 生成之后，输出文件夹将包含下表中所述的文件。  
  
|文件（在 bin 文件夹中）|描述|  
|-----------------------------|-----------------|  
|*Projectname*.asdatabase|包含在部署脚本文件中定义 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中对象的元数据的 ASSL 元素。 部署引擎使用此文件来将对象部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。|  
|*Projectname*.configsettings|包含部署过程中使用的配置设置，可以直接修改或在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导中修改这些设置（例如用于数据源的连接字符串）。|  
|*Projectname*.deploymenttargets|包含部署过程中使用的目标设置，您可以直接修改或在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导中修改这些目标设置（例如服务器名称和数据库名称）。|  
|*Projectname*.deploymentoptions|包含在部署过程中使用的各种选项设置，可以直接修改或在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导中修改这些选项设置（例如存储位置）|  
|*Assemblyname*/*dllname.* dll|用于每个被引用程序集的各个文件夹；每个文件夹包含程序集、被引用程序集以及输出调试信息的所有关联 .pdb 文件的 DLL。|  
  
|文件（在 obj 文件夹中）|描述|  
|-----------------------------|-----------------|  
|\<配置名称 > \LastBuilt.xml|包含用来标识 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目的上次生成时间的时间戳和哈希代码。|  
  
 这些 XML 文件不包含\<创建 > 和\<Alter > 标记中，在部署过程中构造的。  
  
 还会将被引用程序集（不包括标准系统和 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 程序集）复制到输出目录。 引用解决方案中的其他项目时，首先使用相应的项目配置以及由项目引用建立的生成依赖项生成这些项目，然后将这些项目复制到项目输出文件夹。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言（支持 XMLA 的 ASSL）](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [部署 Analysis Services 项目 (SSDT)](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  
