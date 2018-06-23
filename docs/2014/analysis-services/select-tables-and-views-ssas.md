---
title: 选择表和视图 (SSAS) |Microsoft 文档
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
- sql12.asvs.bidtoolset.seltablesviews.f1
ms.assetid: 5e8121cc-03f0-4168-98cf-63c5c032bb0b
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5cdb1c21481e79c98b2d9f7958b54e1d5e2f8745
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017814"
---
# <a name="select-tables-and-views-ssas"></a>选择表和视图 (SSAS)
  **“表导入向导”** 的这一页可用于选择要从其导入数据的表和视图。 若要从 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]访问该向导，请在 **“模型”** 菜单上，单击 **“从数据源导入”**。  
  
 此页上表和视图的外观将不会确保该导入将成功。 如果在“模拟信息”页中指定的用户没有足够的权限从所选数据库中读取，则导入将失败。  
  
 对于使用 Windows 身份验证的数据源，当前用户的凭据用于在“选择表和视图”对话框中提取表和视图。 对于其他数据源，在连接字符串中提供的凭据用于提取数据。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **Server**  
 显示连接到的服务器。  
  
 **“数据库”**  
 显示您选择的数据库。  
  
 **表和视图**  
 列出数据库中的表和视图。 选中要导入的每个表和视图旁边的复选框。  
  
 **源表**  
 基于数据源的类型指定源表的名称。  
  
 **架构**  
 指定包含源表的架构。 根据数据库的类型，架构可作为其他对象（例如表）的容器，并且还可指示这些对象的所有权。  
  
 **友好名称**  
 指定源表的友好名称。 默认情况下，该列显示在 **“源表”** 列中出现的源表的名称。 如果您要使用与源数据库中所用名称不同的名称，请更改该名称。  
  
 **筛选器详细信息**  
 在某一筛选器已应用于要导入的数据时，在“筛选器详细信息”对话框中显示数据导入筛选器。 有关详细信息，请参阅[筛选器详细信息 (SSAS)](filter-details-ssas.md)。  
  
 **预览并筛选**  
 显示“预览选择的表”对话框，该对话框用于将筛选器应用于要导入的数据。 有关详细信息，请参阅[预览选择的表 (SSAS)](preview-selected-table-ssas.md)。  
  
 **选择相关的表**  
 选择与您已经选择的表和视图相关的表和视图以进行导入。  
  
  