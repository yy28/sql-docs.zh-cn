---
title: "从 Power Pivot (SSAS 表格) 导入 |Microsoft 文档"
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
f1_keywords:
- sql13.asvs.bidtoolset.importfromppt.f1
ms.assetid: ac1a6a79-bda3-4122-a717-8b1e2f77da02
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b85ae04b00034decd7390f86db1ee7e00c496434
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="import-from-power-pivot-ssas-tabular"></a>从 Power Pivot 导入（SSAS 表格）
  本主题介绍如何通过使用 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 中的“从 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 导入”项目模板从 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]工作簿导入元数据和数据，来创建新的表格模型项目。  
  
## <a name="create-a-new-tabular-model-from-a-power-pivot-for-excel-file"></a>从 Power Pivot for Excel 文件创建新的表格模型  
 在通过从 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿中导入来创建新的表格模型项目时，将使用定义工作簿结构的元数据来在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中创建和定义表格模型项目的结构。 表、列、度量值和关系之类的对象将与它们处于 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿中一样保留并出现在表格模型项目中。 不对 .xlsx 工作簿文件进行任何更改。  
  
> [!NOTE]  
>  表格模型不支持链接表。 在从包含链接表的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿中导入时，链接表数据将作为复制\粘贴的数据处理并且存储于 Model.bim 文件中。 在查看复制\粘贴的表的属性时，“源数据”属性将被禁用，并且“表”菜单上的“表属性”对话框将被禁用。  
>   
>  对于可添加到在模型中嵌入的数据中的行数，有最多 10,000 行的限制。 如果你在从 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 导入模型时看到错误“数据已被截断。 粘贴的表不能包含超过 10000 行”，则应通过将嵌入的数据移到其他数据源（例如 SQL Server 中的表）中，对该 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 模型进行修订，然后重新导入。  
  
 有一些特别注意事项，这取决于工作区数据库是在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 所处的计算机（本地）上的 Analysis Services 实例中还是在远程 Analysis Services 实例中。  
  
 如果工作区数据库在本地 Analysis Services 实例中，则可以从 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿导入元数据和数据。 从工作簿复制元数据并使用该元数据创建表格模型项目。 然后，从工作簿复制数据并将其存储到项目的工作区数据库中（复制/粘贴的数据除外，该数据存储在 Model.bim 文件中）。  
  
 如果工作区数据库在远程 Analysis Services 实例中，则无法从 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for Excel 工作簿导入数据。 您仍可以导入工作薄元数据；不过，这将导致脚本在远程 Analysis Services 实例中运行。 你应只从受信任的 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作薄导入元数据。 必须从数据源连接所定义的源中导入数据。 必须将 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿中的复制/粘贴的数据和链接表数据复制并粘贴到表格模型项目中。  
  
#### <a name="to-create-a-new-tabular-model-project-from-a-power-pivot-for-excel-file"></a>从 Power Pivot for Excel 文件创建新的表格模型项目  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，在 **“文件”** 菜单上，单击 **“新建”**，然后单击 **“项目”**。  
  
2.  在“新建项目”对话框中，在“已安装的模板”下，单击“商业智能”，然后单击“从 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 导入”。  
  
3.  在  “名称”中，键入项目的名称，然后指定位置和解决方案名称，再单击 “确定”。  
  
4.  在 **“打开”** 对话框中，选择包含您要导入的模型元数据和数据的 [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] 文件，然后单击 **“打开”**。  
  
## <a name="see-also"></a>另请参阅  
 [工作区数据库（SSAS 表格）](../../analysis-services/tabular-models/workspace-database-ssas-tabular.md)   
 [复制和粘贴数据 &#40;SSAS 表格 &#41;](../../analysis-services/tabular-models/ssas-import-data-copy-and-paste-data.md)  
  
  

