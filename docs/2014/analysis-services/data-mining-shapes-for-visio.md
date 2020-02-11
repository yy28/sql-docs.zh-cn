---
title: Visio 数据挖掘形状 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining shapes
- templates [Visio]
- Visio shapes
- shapes, data mining
ms.assetid: 11a821d9-1c0a-442e-b735-92208ce479dc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6ebe206d4f4942e9a9456ba10b00d33514ef6212
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66086399"
---
# <a name="data-mining-shapes-for-visio"></a>Visio 数据挖掘形状
  Visio 数据挖掘形状提供为显示数据挖掘模型而自定义的各种模板。 通过使用这些模板，您可以连接到已创建的模型和创建交互式演示文稿来说明数据挖掘的结果。  
  
 与静态图形和屏幕捕获相比，这些模板具有许多优点，它们与基础数据挖掘模型交互，这些模型存储在 Analysis Services 的实例上，并允许您自定义挖掘模型中的模式的显示方式。 可折叠和展开树模型、对数据节点进行筛选或按属性进行筛选以及显示概率和系数等模型统计信息。  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 Visio 模板包括这些向导：  
  
-   **依赖关系网络关系图：** 使用此向导可以为决策树和神经网络创建关系图。  
  
-   **决策树关系图：** 使用此向导创建显示与决策树模型关联的决策点和公式的关系图。 此关系图还可用于回归模型。  
  
-   **分类关系图：** 使用此向导为分段模型创建彩色图形。 您可以在两个视图间切换（如属性对比、分类剖面图和依赖关系），并自定义分类的外观。  
  
## <a name="installation"></a>安装  
 安装 Visio 数据挖掘模板时，默认情况下会将以下文件安装到\<驱动器> \program Files\Microsoft SQL SERVER 2012 DM 外接程序（或\<驱动器> \ 或 Program files （x86） \Microsoft SQL Server 2012 DM 外接程序）：  
  
-   **Microsoft 数据挖掘**此模板包含预先设计的格式设置、布局和向导，可帮助您使用数据挖掘形状。  
  
-   **Microsoft 数据挖掘形状 Studio .vss**此模具文件包含与模板关联的形状。  
  
## <a name="how-to-use-the-templates"></a>如何使用模型模板  
 若要打开模板，可双击形状文件，也可打开 Visio，然后打开形状模板。  
  
1.  将一个 Visio 数据挖掘形状从模具放到新页上。  
  
2.  在向导启动时，连接到具有要显示的数据挖掘模型的服务器。  
  
3.  选择该数据挖掘模型，将模型的类型与可视化类型相匹配。  
  
4.  设置应如何显示数据以及确定数据格式的选项。  
  
5.  完成**数据挖掘形状向导**后，可以使用 Visio 的功能修改和增强关系图。  
  
 有关如何使用和增强 Visio 模型关系图的详细信息，请参阅[在 visio 中查看数据挖掘模型 &#40;数据挖掘外接程序&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md)  
  
## <a name="requirements"></a>要求  
  
-   若要使用这些模板，您首先必须创建与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的连接。  
  
     该向导将会提示您选择 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器，并指定包含数据挖掘模型的数据库。  
  
     有关如何创建连接的信息，请参阅[连接到源数据 &#40;Excel 数据挖掘客户端&#41;](connect-to-source-data-data-mining-client-for-excel.md)。  
  
-   如果使用的是表分析工具，请确保将模型保存到[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]服务器，且不要使用临时模型。  
  
-   必须已使用所支持的某种算法创建模型：聚类、决策树、神经网络、Naïve Bayes 或逻辑回归。  
  
  
