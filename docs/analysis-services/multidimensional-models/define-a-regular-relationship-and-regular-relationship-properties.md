---
title: 定义常规关系和常规关系属性 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9ee79742f919d7f47ae73968666d96622e3429bc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34022274"
---
# <a name="define-a-regular-relationship-and-regular-relationship-properties"></a>定义常规关系和常规关系属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在定义新的多维数据集维度或新的度量值组时， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将试图检测是否存在常规关系并将维度用法设置为 **Regular**。 您可以在多维数据集设计器的 **“维度用法”** 选项卡中查看或编辑常规维度关系。  
  
 当您定义多维数据集维度与度量值组的关系时，也会指定该关系的粒度属性。 粒度属性定义了该维度在多维数据集中可用的最低详细级别，此粒度属性通常是指维度的键属性。 但是，有时您可能希望将特定度量值组中特定多维数据集维度的粒度设置为其他粒度。 例如，如果您正在使用“销售配额”或“预算”度量值组，则可能希望将“时间”维度的粒度属性设置为“月”属性，而不是“日”属性。 当您将粒度属性指定为键属性以外的属性时，必须确保维度中的所有其他属性都能通过属性关系直接或间接地链接到该属性。 如果不能， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将无法正确地聚合数据。  
  
  
