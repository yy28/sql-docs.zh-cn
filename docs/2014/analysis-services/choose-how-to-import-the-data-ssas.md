---
title: 选择如何导入数据 (SSAS) |Microsoft 文档
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
- sql12.asvs.bidtoolset.choosehowtoimpdata.f1
ms.assetid: 17dc6903-c239-46aa-a3b0-6e3156accacc
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9929f61537fdf635ffd130b75d9e2738be256aab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130245"
---
# <a name="choose-how-to-import-the-data-ssas"></a>选择如何导入数据 (SSAS)
  **“表导入向导”** 的这一页可用于选择从所选数据源导入数据的方式。 若要从 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]访问该向导，请在 **“模型”** 菜单上，单击 **“从数据源导入”**。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **从表和视图的列表中选择以选择要导入数据**  
 如果要通过从列表中选择来导入数据，请选择此选项。  
  
> [!NOTE]  
>  仅当所选数据源公开“表导入向导”支持的架构信息后，此选项才可用。  
  
 **编写查询以指定要导入的数据**  
 如果要使用 SQL 查询来导入数据，请选择此选项。 SQL 查询可以处理导入的数据。 例如，您可以联接来自不同表的数据，或仅选择符合特定条件的行。  
  
  