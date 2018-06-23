---
title: 常规 （数据库设计器） (Analysis Services-多维数据) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.databasedesigner.dbconfigurationpane.f1
helpviewer_keywords:
- Database Designer
ms.assetid: 00c9c42b-db2b-4620-8fb6-1e165ff0cbdd
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 435817b44643ddf1d3e6703ca2872dd5afe407c5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127200"
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
  
 **Description**  
 输入对数据库的说明。  
  
## <a name="translations-options"></a>翻译选项  
 展开 **“翻译”** 部分可以创建和修改数据库标题和说明的翻译。 本部分包含带有以下列的网格：  
  
 **语言**  
 为指定事务选择语言。  
  
 若要将一个新翻译添加到网格中，单击**\<添加新翻译 >**。  
  
 **翻译后的标题**  
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
  
  