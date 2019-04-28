---
title: 连接到平面文件 (SSAS) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connflatfile.f1
ms.assetid: a365991e-eded-4cd8-89c0-0daf6d658d15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1b3fa68b63e9ccf1a11712192d675c46ece7a86b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62680304"
---
# <a name="connect-to-a-flat-file-ssas"></a>连接到平面文件 (SSAS)
  “表导入向导”的这一页可用于连接到平面文件 (.txt)、制表符分隔的文件 (.tab) 或逗号分隔的文件 (.csv)。 若要从 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]访问该向导，请在 **“模型”** 菜单上，单击 **“从数据源导入”**。  
  
 若要连接到平面文件，必须在计算机上安装 ACE 访问接口。 有关详细信息，请参阅[数据源支持（SSAS 表格）](tabular-models/data-sources-supported-ssas-tabular.md)。  
  
> [!NOTE]  
>  在此页中选择文件时，将使用当前用户的凭据。 但是，如果在“模拟信息”页中指定的用户没有足够的权限从所选文件中读取，则导入将不会成功。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **友好连接名称**  
 键入此数据源连接的唯一名称。 这是必填字段。  
  
 **文件路径**  
 指定文件的完整路径。  
  
 **“浏览”**  
 导航至文件可用的位置。  
  
 **Column Separator**  
 从可用列分隔符的列表中进行选择。 选择不可能出现在文本中的分隔符。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|制表符 (t)|列由制表符 (t) 分隔。|  
|逗号 (,)|列由逗号 (,) 分隔。|  
|分号 (;)|列由分号 (;) 分隔。|  
|空格 ( )|列由空格 ( ) 分隔。|  
|冒号 (:)|列由冒号 (:) 分隔。|  
|竖线 (|)|列由竖线 (|) 分隔。|  
  
 **高级**  
 为平面文件指定编码和区域设置选项。  
  
 **使用第一行作为列标题**  
 指定是否要使用第一个数据行作为目标表的列标题。  
  
 **数据预览**  
 预览所选文件中的数据，并且使用以下选项修改数据导入。  
  
> [!NOTE]  
>  只有文件中的前 50 行显示在此预览。  
  
|Option|Description|  
|------------|-----------------|  
|**列标题中的复选框**|选中该复选框可在数据导入中包括列。 取消选中该复选框则从数据导入中删除列。|  
|**列标题中的向下箭头按钮**|对列中的数据进行排序和筛选。|  
  
 **清除行筛选器**  
 删除已应用于列中数据的所有筛选器。  
  
  
