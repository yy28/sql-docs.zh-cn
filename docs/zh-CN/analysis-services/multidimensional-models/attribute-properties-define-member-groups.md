---
title: 定义成员组 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 15e02bff085d6a53d3573cbb354948b101a67513
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="attribute-properties---define-member-groups"></a>特性属性-定义成员组
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  如果属性有很多成员，可以选择将这些成员分组到存储桶中，以减少用户在浏览某个层次结构中的数据时看到的成员数。 确定用于放置成员组的存储桶的数目，并为存储桶设置命名架构。 有关详细信息，请参阅[对属性成员分组（离散化）](../../analysis-services/multidimensional-models/attribute-properties-group-attribute-members.md)。  
  
 可以通过设置 **DiscretizationMethod** 属性来将成员分组，该属性可通过 **中的** “属性” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]窗口访问。  
  
 创建成员组时，所做更改只有在处理了维度后才能供用户使用。 有关详细信息，请参阅[处理多维模型 (Analysis Services)](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
### <a name="to-create-member-groups"></a>创建成员组  
  
1.  打开要使用的维度。 默认情况下，将打开 **“维度结构”** 选项卡。  
  
2.  在“属性”中，右键单击要对其成员进行分组的属性，再单击“属性”。  
  
3.  从 **DiscretizationMethod** 旁边的下拉列表中，选择对成员分组时所用的方法。 有关 **DiscretizationMethod** 设置的详细信息，请参阅[对属性成员分组（离散化）](../../analysis-services/multidimensional-models/attribute-properties-group-attribute-members.md)。  
  
  
