---
title: 属性 （维度结构选项卡，维度设计器） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.attributespane.f1
ms.assetid: 627eaa08-7638-4edd-bdfa-0d8175a7cde5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a9eab7de49abaf06446fbd03f7b80c381d102f20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66064403"
---
# <a name="attributes-dimension-structure-tab-dimension-designer-analysis-services---multidimensional-data"></a>属性（“维度结构”选项卡，维度设计器）（Analysis Services - 多维数据）
  可以使用此窗格管理与所选维度关联的属性。 可以将属性从此窗格拖到 **“层次结构”** 窗格，以创建层次结构和级别。 有关详细信息，请参阅[层次结构&#40;维度结构选项卡，维度设计器&#41; &#40;Analysis Services-多维数据&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md)。  
  
 若要创建属性，请在处于列表模式、树模式或视图模式时，将相应的列从 **“数据源视图”** 窗格拖到 **“属性”** 窗格中。 若要删除属性，请从快捷菜单中选择 **“删除”** 。  
  
 **若要显示属性窗格**  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 项目，然后打开所需的维度。  
  
2.  如果未选定维度，请单击 **“维度结构”** 选项卡。  
  
## <a name="options"></a>选项  
 **属性**  
 显示所选维度可用的属性。 可以在以下模式中查看此选项：  
  
-   列表模式  
  
     使用此模式可以创建和修改层次结构。 若要在列表模式下查看属性，请从快捷菜单中选择 **“属性显示方式”** ，然后单击 **“列表”** 。  
  
-   树模式  
  
     使用此模式可以创建和修改层次结构。 若要在树模式下查看属性，请从快捷菜单中选择 **“属性显示方式”** ，然后单击 **“树”** 。  
  
-   网格模式  
  
     使用此模式可以手动创建维度或修改特性属性。 若要在网格模式下查看属性，请从快捷菜单中选择 **“属性显示方式”** ，然后单击 **“网格”** 。  
  
## <a name="grid-mode-options"></a>网格模式选项  
 在网格模式中查看属性时，可以访问下表中所列出的列：  
  
 **名称**  
 显示属性的名称。  
  
 **Usage**  
 设置所选属性的用法。 单击下箭头可以从下列选项中进行选择：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|Regular|标识常规属性。|  
|Key|标识维度的键属性。 此项对应于维度的叶成员。 每个维度只能有一个键属性。 若要修改此项，请在“属性”  窗格中单击“KeyColumns”  属性旁边的省略号按钮 ( **...** )。|  
|Parent|表示父子关系中的父属性。 此关系中的子属性必须始终为键属性。|  
|AccountType|表示帐户类型属性。 当度量值的聚合函数设置为“by account”时，服务器或引擎将使用此项。|  
  
 **类型**  
 设置属性的类型。 单击下箭头可以从可用的选项中进行选择。  
  
 **键列**  
 显示基础列的数据类型。 创建新属性时，单击下箭头可以从可用的选项中进行选择。  
  
 **名称列**  
 显示基础列的位置。 创建新属性时，单击下箭头可以选择 **“与键相同”** 或 **“单独列”** 。 如果选择了 **“单独列”** ， **“属性”** 窗格中的 **NameColumn** 属性将设置存储相应名称的列以用于该属性。  
  
## <a name="see-also"></a>请参阅  
 [维度结构&#40;维度设计器&#41; &#40;Analysis Services-多维数据&#41;](dimension-structure-dimension-designer-analysis-services-multidimensional-data.md)   
 [层次结构&#40;维度结构选项卡，维度设计器&#41; &#40;Analysis Services-多维数据&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md)   
 [工具栏&#40;维度结构选项卡，维度设计器&#41; &#40;Analysis Services-多维数据&#41;](toolbar-dimension-structure-designer-analysis-services-multidimensional-data.md)  
  
  
