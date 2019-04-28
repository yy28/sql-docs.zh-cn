---
title: Visio 数据挖掘形状 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
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
ms.openlocfilehash: 92630f90d7b18ad668dcffc02feeb65990cf3c84
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62689997"
---
# <a name="data-mining-shapes-for-visio"></a>Visio 数据挖掘形状
  Visio 数据挖掘形状提供为显示数据挖掘模型而自定义的各种模板。 通过使用这些模板，您可以连接到已创建的模型和创建交互式演示文稿来说明数据挖掘的结果。  
  
 模板提供许多优于静态图表和屏幕捕获-它们与 Analysis Services 实例存储的基础数据挖掘模型进行交互，让您自定义挖掘模型中的模式的显示方式。 可折叠和展开树模型、对数据节点进行筛选或按属性进行筛选以及显示概率和系数等模型统计信息。  
  
 ![DM](media/dm-stencil.gif "DM")  
  
 Visio 模板包括这些向导：  
  
-   **依赖关系网络关系图：** 使用此向导为决策树和神经网络创建图形。  
  
-   **决策树关系图：** 使用此向导创建图表，其中显示的决策点和决策树模型相关联的公式。 此关系图还可用于回归模型。  
  
-   **分类关系图：** 使用此向导创建为分段模型的彩色图形。 您可以在两个视图间切换（如属性对比、分类剖面图和依赖关系），并自定义分类的外观。  
  
## <a name="installation"></a>安装  
 当你安装 Visio 数据挖掘模板时，默认情况下以下文件安装到\<驱动器 > files\microsoft SQL Server 2012 DM Add-ins (或\<驱动器 > \ 或 Program Files (x86) \Microsoft SQL Server 2012 DMAdd-Ins):  
  
-   **Microsoft Data Mining.vst**此模板包含预先设计的格式设置、 布局和向导，可帮助您使用数据挖掘形状。  
  
-   **Microsoft Data Mining Shape Studio.vss**此模具文件包含与模板相关联的形状。  
  
## <a name="how-to-use-the-templates"></a>如何使用模板  
 若要打开模板，可双击形状文件，也可打开 Visio，然后打开形状模板。  
  
1.  将一个 Visio 数据挖掘形状从模具放到新页上。  
  
2.  在向导启动时，连接到具有要显示的数据挖掘模型的服务器。  
  
3.  选择该数据挖掘模型，将模型的类型与可视化类型相匹配。  
  
4.  设置应如何显示数据以及确定数据格式的选项。  
  
5.  完成后**数据挖掘形状向导**，有的关系图，可以修改和增强使用 Visio 的功能。  
  
 有关如何使用和增强 Visio 模型关系图的详细信息，请参阅[查看数据挖掘模型在 Visio 中&#40;数据挖掘外接程序&#41;](viewing-data-mining-models-in-visio-data-mining-add-ins.md)  
  
## <a name="requirements"></a>要求  
  
-   若要使用这些模板，您首先必须创建与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的连接。  
  
     该向导将会提示您选择 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器，并指定包含数据挖掘模型的数据库。  
  
     有关如何创建连接的信息，请参阅[连接到源数据&#40;Excel 数据挖掘客户端&#41;](connect-to-source-data-data-mining-client-for-excel.md)。  
  
-   如果使用表分析工具，请确保保存模型[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]服务器，而不要使用临时模型。  
  
-   必须已使用所支持的某种算法创建模型：聚类、决策树、神经网络、Naïve Bayes 或逻辑回归。  
  
  
