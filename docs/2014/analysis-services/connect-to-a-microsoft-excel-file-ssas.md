---
title: 连接到 Microsoft Excel 文件 (SSAS) |Microsoft 文档
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
- sql12.asvs.bidtoolset.connexcelfile.f1
ms.assetid: 126f7d6b-d270-40e7-b23e-8d114f87065b
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 48de9fd006c3918a23227a097743a95e138b577e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026666"
---
# <a name="connect-to-a-microsoft-excel-file-ssas"></a>连接到 Microsoft Excel 文件 (SSAS)
  **“表导入向导”** 的这一页可用于连接到在本地计算机上存储的 Microsoft Excel 文件。 若要从 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]访问该向导，请在 **“模型”** 菜单上，单击 **“从数据源导入”**。  
  
 若要连接到 Microsoft Excel 文件，必须在计算机上安装适当的 ACE 访问接口。 有关详细信息，请参阅[数据源支持（SSAS 表格）](tabular-models/data-sources-supported-ssas-tabular.md)。  
  
> [!NOTE]  
>  在此页中选择文件时，将使用当前用户的凭据。 但是，如果在“模拟信息”页中指定的用户没有足够的权限从所选文件中读取，则导入将不会成功。  
  
## <a name="uielement-list"></a>UIElement 列表  
 **友好连接名称**  
 键入此数据源连接的唯一名称。 这是必填字段。  
  
 **Excel 文件路径**  
 指定 Excel 文件的完整路径。  
  
 **“浏览”**  
 导航至 Excel 文件可用的位置。  
  
 **高级**  
 通过使用“设置高级属性”对话框设置附加的连接属性。  
  
 **使用第一行作为列标题**  
 指定是否要使用第一个数据行作为目标表的列标题。  
  
 **测试连接**  
 使用当前设置尝试建立与数据源的连接。 将显示一个消息，指示连接是否成功。  
  
  