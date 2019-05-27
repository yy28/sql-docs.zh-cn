---
title: 常规 （数据库设计器） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.databasedesigner.dbconfigurationpane.f1
helpviewer_keywords:
- Database Designer
ms.assetid: 00c9c42b-db2b-4620-8fb6-1e165ff0cbdd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bf87f2441488810286523a75137a3285aabc1956
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081084"
---
# <a name="general-database-designer-analysis-services---multidimensional-data"></a>常规（数据库设计器）（Analysis Services - 多维数据）
  可以使用 **“常规”** 选项卡更改 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库的属性。  
  
 **若要显示常规选项卡**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目。  
  
2.  在“解决方案资源管理器”中，右键单击 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目，单击“编辑数据库”，然后单击“常规”选项卡。  
  
## <a name="basic-options"></a>基本选项  
 展开 **“基本”** 部分可以修改数据库的基本信息。 本部分包含以下选项：  
  
 **数据库名称**  
 显示数据库的名称。  
  
> [!NOTE]  
>  若要重命名该数据库，请在“解决方案资源管理器”中，右键单击相应的项目，然后单击“属性”。 在数据库的 **“属性页”** 对话框的 **“部署”** 页上，将 **“数据库”** 属性的值更改为新的数据库名称。  
  
 **说明**  
 输入对数据库的说明。  
  
## <a name="translations-options"></a>翻译选项  
 展开 **“翻译”** 部分可以创建和修改数据库标题和说明的翻译。 本部分包含带有以下列的网格：  
  
 **语言**  
 为指定事务选择语言。  
  
 若要向网格中添加一个新的翻译，请单击**\<添加新翻译 >**。  
  
 **已翻译的标题**  
 以翻译的相应语言键入数据库的标题。 如果为空，将使用默认的数据库标题。  
  
 **已翻译的说明**  
 以翻译的相应语言键入对数据库的说明。 如果为空，将使用默认的数据库说明。  
  
## <a name="account-type-mapping-options"></a>帐户类型映射选项  
 展开 **“帐户类型映射”** 部分，可以修改与所选数据库中每个帐户 **“类型”** 相关联的默认聚合函数。  
  
> [!NOTE]  
>  此选项仅适用于一个或多个度量值使用 *ByAccount* 聚合函数的多维数据集。  
  
 本部分包含带有以下列的网格：  
  
 **名称**  
 键入帐户类型的名称。  
  
 若要添加新的帐户类型，请单击**\<添加新帐户类型 >**。  
  
 **别名**  
 设置帐户类型的默认名称，以供商业智能向导使用。 如果此列为空，则将使用默认的 **“名称”** 列。  
  
 **聚合函数**  
 选择用于所选帐户类型的聚合函数。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [多维模型数据库&#40;SSAS&#41;](multidimensional-models/multidimensional-model-databases-ssas.md)   
 [警告&#40;数据库设计器&#41; &#40;Analysis Services-多维数据&#41;](warnings-database-designer-analysis-services-multidimensional-data.md)  
  
  
