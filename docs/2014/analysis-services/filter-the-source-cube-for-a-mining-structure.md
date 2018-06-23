---
title: 筛选挖掘结构的源多维数据集 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- slice cubes [Analysis Services]
- mining structures [Analysis Services], filtering source cube
- cubes [Analysis Services], slicing
- filtering data [Analysis Services]
ms.assetid: 05dce7e1-2fe5-4500-bacf-c1a8a76e1424
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ed1ff70d4bb0f0ebd20da468c91f2603318ec217
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124669"
---
# <a name="filter-the-source-cube-for-a-mining-structure"></a>筛选挖掘结构的源多维数据集
  当你创建基于多维模型 （OLAP 多维数据集） 中的数据的挖掘结构时，你可以*切片*基于挖掘结构的多维数据集。 通过切片操作可创建数据子集，作为用于给挖掘模型定型的数据的一种筛选器。  
  
### <a name="to-slice-a-cube"></a>对多维数据集进行切片  
  
1.  数据挖掘设计器中[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]，选择**挖掘结构**选项卡或**挖掘模型**选项卡。  
  
2.  上**挖掘模型**菜单上，选择**定义挖掘结构多维数据集切片**。  
  
     **多维数据集切片**对话框随即打开。  
  
3.  在**维度**列**多维数据集切片**对话框框中，选择你想要筛选的维度。  
  
4.  选择使用的列表中的层次结构级别**层次结构**列。  
  
5.  从列表中选择一个运算符**运算符**列中，要在生成筛选器条件中使用。  
  
6.  单击中的框**筛选器**列。  
  
     此时将打开包含层次结构指定级别中的所有成员的对话框。  
  
7.  选择您要进行筛选的成员。  
  
8.  单击**确定**成员对话框中。  
  
9. 单击**确定**中**多维数据集切片**对话框。  
  
     现在根据多维数据集切片的定义对源多维数据集进行筛选。  
  
## <a name="see-also"></a>请参阅  
 [挖掘结构任务和操作指南](data-mining/mining-structure-tasks-and-how-tos.md)   
 [创建新的 OLAP 挖掘结构](data-mining/create-a-new-olap-mining-structure.md)  
  
  