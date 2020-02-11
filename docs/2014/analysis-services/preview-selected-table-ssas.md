---
title: 预览选定的表（SSAS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.previewselecttable.f1
ms.assetid: b6b34b5a-43b3-4a75-9f3b-b2ad1084b1b6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a0f168dabd237fe685eb90d2caeeba0db4eed97
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070723"
---
# <a name="preview-selected-table-ssas"></a>预览选择的表 (SSAS)
  
  **“表导入向导”** 的这一页可用于预览所选表中的数据，选择要在数据导入中包括的列，并且筛选所选列中的数据。 若要从 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]访问该向导，请在 **“模型”** 菜单上，单击 **“从数据源导入”**。  
  
 不是表中的所有行都显示。 但是，在导入过程中，您设置的筛选器将应用于表中的所有数据。  
  
 对于使用 Windows 身份验证的数据源，当前用户的凭据用于提取在“预览并筛选”对话框中显示的数据。 对于其他数据源，在连接字符串中提供的凭据用于提取数据。  
  
 此页上数据的外观将不会确保导入将成功。 如果在“模拟信息”页中指定的用户名没有足够的权限从所选数据库中读取，则导入将失败。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **列标题中的复选框**  
 选中该复选框可在数据导入中包括列。 取消选中该复选框则从数据导入中删除列。  
  
 **列标题中的下箭头按钮**  
 筛选列中的数据。  
  
 **清除行筛选器**  
 删除已应用于列中数据的所有筛选器。  
  
  
