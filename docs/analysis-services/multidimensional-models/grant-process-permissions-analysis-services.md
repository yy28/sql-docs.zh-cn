---
title: "授予处理权限 (Analysis Services) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- permissions [Analysis Services], process
- process permissions [Analysis Services]
ms.assetid: c1531c23-6b46-46a8-9ba3-b6d3f2016443
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7f1542d477a10e6a77e67e24d607b7086da1bb55
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="grant-process-permissions-analysis-services"></a>授予处理权限 (Analysis Services)
  作为管理员，你可以创建专用于 Analysis Services 处理操作的角色，从而可以委派特定任务到其他用户，或者委派到用于无人参与的预定处理的应用程序。 可以在数据库、多维数据集、维度和挖掘结构级别授予处理权限。 除非你正在使用非常大型的多维数据集或表格数据库工作，否则我们建议授予数据库级别的处理权限，包括所有对象，也包括彼此互有相关性的对象。  
  
 权限通过角色授予，将对象与权限以及 Windows 用户或组帐户进行关联。 请记住，权限是可以累加的。 如果一个角色授予处理多维数据集的权限，同时另一个角色授予同一用户处理维度的权限，那么两个不同角色的权限会合并以授予用户在该数据库内的处理多维数据集和处理特定维度的权限。  
  
> [!IMPORTANT]  
>  其角色只有处理权限的用户将不能够使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 来连接 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和处理对象。 这些工具要求 **Read Definition** 访问对象元数据的权限。 没有功能使用任一工具时，则必须使用 XMLA 脚本来执行处理操作。  
>   
>  我们建议同时授予 **Read Definition** 权限以便进行检测。 具有 **读取定义** 和 **处理数据库** 权限的用户可交互地处理 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的对象。 有关详细信息，请参阅 [授予对象元数据的读取定义权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md) 。  
  
## <a name="set-processing-permissions-at-the-database-level"></a>设置数据库级别的处理权限  
 此部分解释了如何通过非管理员为数据库中的所有多维数据集、维度、挖掘结构和挖掘模型启用处理。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的实例，打开“数据库”文件夹，并选择一个数据库。  
  
2.  右键单击**角色** | **新角色**。 输入名称和说明。  
  
3.  在“常规”  窗格，选择“处理数据库”  复选框。 此外，选择“读取定义”  也可以通过其中一个 SQL Server 工具（例如， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]）启用交互式处理。  
  
4.  在“成员身份”  窗格，添加有权限处理此数据库中的任何对象的 Windows 用户和组帐户。  
  
5.  单击“确定”  ，完成角色定义。  
  
## <a name="set-processing-permissions-on-individual-objects"></a>设置单个对象的处理权限  
 你可设置单个多维数据集、维度、数据挖掘结构或模型的处理权限。  
  
 如果你无意中排除了需要一起处理的对象（例如，如果启用了对多维数据集进行处理而未对其相关维度进行处理），处理会失败。 因为很容易就会漏掉对象相关性，所以设置单个对象的处理权限时，完全测试是至关重要的。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的实例，打开“数据库”文件夹，并选择一个数据库。  
  
2.  右键单击**角色** | **新角色**。 输入名称和说明。  
  
3.  在“常规”  窗格，清除“处理数据库”  复选框。 数据库权限通过使角色选项显示为灰色或不可选来覆盖在更低级别对象上设置权限的功能。  
  
     技术上来说，专用处理角色不需要数据库权限。 但如果没有数据库级别的“读取权限”  ，则无法查看 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的数据库，这会让测试更加困难。  
  
4.  选择单个对象来处理：  
  
    -   在“多维数据集”  窗格，为每个多维数据集选中“处理”  复选框。  
  
    -   在“维度”  窗格，选择“所有数据库维度” ，然后为每个维度选中“处理”  复选框。 或者，选择所有行，然后使用 Shift + 单击来切换复选框选项。  
  
5.  在“成员身份”  窗格，添加有权限处理这些对象的 Windows 用户和组帐户。  
  
6.  单击“确定”  ，完成角色定义。  
  
## <a name="test-processing"></a>测试处理  
  
1.  按住 Shift 键并右键单击 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，选择“以不同用户身份运行”并使用分配到正在进行测试的角色的 Windows 帐户连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的实例。  
  
2.  打开“数据库”文件夹，选择一个数据库。 你将只会看见对角色可见的数据库，你的帐户具有此角色的成员身份。  
  
3.  右键单击多维数据集或维度并选择“处理”。 选中处理选项。 为对象的所有组合测试所有选项。 如果由于缺失对象而出现错误，请添加对象到角色。  
  
## <a name="set-processing-permissions-on-a-data-mining-structure"></a>设置数据挖掘结构的处理权限  
 你可以创建一个授予处理数据挖掘结构权限的角色。 这包括处理所有挖掘模型。  
  
 用于浏览挖掘模型和结构的“钻取” 和“读取定义”  权限是原子的且可被添加到同一角色或者被分隔到不同角色。  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]的实例，打开“数据库”文件夹，并选择一个数据库。  
  
2.  右键单击**角色** | **新角色**。 输入名称和说明。 在“常规”  窗格，确保数据库权限复选框处于清空状态。 数据库权限将通过使角色选项显示为灰色或不可选来覆盖在更低级别对象上设置权限的功能。  
  
3.  在“挖掘结构”  窗格，为每个挖掘结构选中“处理”  复选框。  
  
4.  在“成员身份”  窗格，添加有权限处理此数据库中的任何对象的 Windows 用户和组帐户。  
  
5.  单击“确定”  ，完成角色定义。  
  
## <a name="see-also"></a>另请参阅  
 [处理数据库、表或分区 (Analysis Services)](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)   
 [处理多维模型 (Analysis Services)](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [授予数据库权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)   
 [授予对象元数据的读取定义权限 (Analysis Services)](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md)  
  
  

