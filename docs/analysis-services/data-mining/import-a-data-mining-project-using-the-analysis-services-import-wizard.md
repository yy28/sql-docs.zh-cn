---
title: 导入数据挖掘项目使用 Analysis Services 导入向导 |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 52e98d6916b66c4ab26b2791d023d25bffc4cab8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63043954"
---
# <a name="import-a-data-mining-project-using-the-analysis-services-import-wizard"></a>使用 Analysis Services 导入向导导入数据挖掘项目
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  本主题介绍如何通过使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的模板“从服务器导入（多维和数据挖掘）项目”从另一台服务器上的现有数据挖掘项目导入元数据，来创建新的数据挖掘项目。  
  
## <a name="import-data-sources-mining-structures-and-mining-models-from-an-existing-data-mining-project"></a>从现有数据挖掘项目导入数据源、挖掘结构和挖掘模型  
 在使用模板“从服务器导入（多维和数据挖掘）项目”时，[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 会创建一个新的数据挖掘项目，然后从指定的数据挖掘项目复制元数据。 该新项目包含与从中进行导入的 ssASnoversion 数据库相同的数据源、数据源视图、挖掘结构和挖掘模型。 但是，在您更新特定属性并处理对象之前将无法使用该项目，如下所述：  
  
-   数据本身不从从源服务器复制到新的数据挖掘项目仅导入的数据源和数据源视图的定义。 因此，在完成导入过程并创建对象后，您必须通过定型挖掘结构和依赖模型来用数据填充对象。 可以在数据挖掘设计器中使用命令 **“全部处理”** 来定型模型和结构。  
  
-   如果您导入的是已在早期版本的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中创建的项目，则数据源可能会使用项目要导入到的服务器上未安装的访问接口。 如果处理导入的挖掘结构时出错，请右键单击每个数据源并选择“打开设计器”以编辑连接字符串和查看提供程序属性。  
  
     此时，您可能还需要验证要用于处理数据挖掘对象或查询数据挖掘模型的帐户是否具有对数据源的必要权限。  
  
-   默认情况下，在导入项目时，工作区数据库会设置为本地主机，或者任意默认实例会在 **中配置为** “默认目标服务器” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。 若要设置此属性，请从 **“选项”** 菜单中依次选择 **“商业智能设计器”**、 **“Analysis Services”** 和 **“常规”**。  
  
     请注意， [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中还包含一个单独选项，可设置此选项以便为 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 表格模型项目配置默认部署服务器。 **“默认部署服务器”** 设置可确定表格模型项目的默认工作区数据库。 不能对数据挖掘项目使用支持表格模型的实例  
  
     如果无法更改默认部署数据库以使用在多维或数据挖掘模式下运行的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例，则可始终通过使用 **“项目属性”** 对话框来指定部署数据库。  
  
#### <a name="to-create-a-new-data-mining-project-by-importing-an-existing-data-mining-project"></a>通过导入现有数据挖掘项目来创建新的数据挖掘项目  
  
1.  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中，在 **“文件”** 菜单上，单击 **“新建”**，然后单击 **“项目”**。  
  
2.  在“新建项目”对话框中，在“已安装的模板”下，依次单击“商业智能”、“Analysis Services”和“从服务器导入（多维/数据挖掘）”。  
  
3.  在 **“名称”** 中，键入项目的名称，然后指定位置和解决方案名称，再单击 **“确定”**。  
  
     这将启动 **“导入 Analysis Services 数据库向导”** 。 单击“欢迎使用”页面上的“确定”以继续。  
  
4.  在该页上的 **“选择源数据库”** 中，对于 **“服务器”**，指定包含要导入的解决方案的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。  
  
     对于 **“数据库”**，选择包含要导入的数据挖掘对象的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。  
  
    > [!WARNING]  
    >  无法指定要导入的对象；在选择现有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库时，会导入所有多维和数据挖掘对象。  
  
     单击“下一步” 。  
  
5.  **“完成向导”** 页将显示导入操作的进度。 无法取消该操作或更改正在导入的对象。 完成操作后，请单击 **“完成”** 。  
  
     这将自动使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]打开新对象。  
  
## <a name="see-also"></a>请参阅  
 [项目属性](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)  
  
  
