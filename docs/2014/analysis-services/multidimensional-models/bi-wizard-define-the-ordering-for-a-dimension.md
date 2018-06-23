---
title: 定义维度的排序 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- OrderBy property
- dimensions [Analysis Services], ordering
- Business Intelligence enhancements [Analysis Services], ordering
- dimensions [Analysis Services], Business Intelligence enhancements
- ordering dimensions [Analysis Services]
- OrderByAttributeID property
ms.assetid: c42fbd58-244d-4e0a-b715-6f919cbc3ad9
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d9a0fa0464c2263d21e50fa53c3b577a42d0a950
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126936"
---
# <a name="define-the-ordering-for-a-dimension"></a>定义维度的排序
  可通过将属性排序增强功能添加到多维数据集或维度中，指定属性成员的排序方式。 成员可以按属性的名称或键进行排序，也可以按另一个属性的名称或键基于属性关系进行排序。 默认情况下，成员按名称排序。 此增强功能更改`OrderBy`和`OrderByAttributeID`维度中的属性的属性设置。  
  
 若要添加属性排序功能，可以使用商业智能向导，并在 **“选择增强功能”** 页中选择 **“指定属性顺序”** 选项。 然后，此向导将指引您完成相应的步骤，以选择要应用属性排序的维度，并指定如何对所选维度的属性进行排序。  
  
## <a name="selecting-a-dimension"></a>选择维度  
 在向导的第一个 **“指定属性顺序”** 页上，指定要应用属性排序的维度。 添加到此所选维度中的属性排序增强功能将导致维度发生更改。 所有包含选定维度的多维数据集都将继承这些更改。  
  
## <a name="specifying-ordering"></a>指定顺序  
 在向导的第二个 **“指定属性顺序”** 页上，指定维度中的所有属性将如何进行排序。  
  
 在 **“排序依据属性”** 列中，可以更改用来进行排序的属性。 如果你想要使用的成员进行排序的属性不在列表中，向下滚动列表，，然后选择**\<新属性...>** 以打开**选择一列**对话框中，您可以在其中维度表中选择一个列。 如果使用 **“选择列”** 对话框来选择列，则可以创建可用来对属性的成员进行排序的其他属性。  
  
 然后，可以在 **“条件”** 列中选择按 **“键”** 还是按 **“名称”** 来对属性的成员进行排序。  
  
  