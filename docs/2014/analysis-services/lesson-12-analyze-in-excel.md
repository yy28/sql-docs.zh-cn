---
title: 第13课：在 Excel 中分析 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ce717071-193b-4c99-9654-c7a613e16327
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6a1564a2b190703e011624162ad4bc25fd5de794
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66079193"
---
# <a name="lesson-13-analyze-in-excel"></a>第 13 课：在 Excel 中分析
  在本课中，您将使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中的“在 Excel 中分析”功能打开 Microsoft Excel、自动创建到模型工作区的数据源连接以及自动将数据透视表添加到工作表。 “在 Excel 中分析”功能提供一种快速简单的方法在部署模型之前测试模型的功效。 在本课中，将执行数据分析。 本课的目的是让你（模型作者）熟悉可以用来测试模型设计的工具。 与模型作者使用“在 Excel 中分析”功能所不同的是，最终用户将使用客户端报告应用程序（如 Excel 或 [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)] ）来连接和浏览部署的模型数据。  
  
 为了完成此课程，Excel 必须与 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]安装在同一台计算机上。 若要了解详细信息，请参阅[在 Excel 中分析（SSAS 表格）](tabular-models/analyze-in-excel-ssas-tabular.md)。  
  
 本课预计完成时间：**20 分钟**  
  
## <a name="prerequisites"></a>先决条件  
 本主题是表格建模教程的一部分，应当按顺序完成。 在执行本课程中的任务之前，须已完成上一课： [第 11 课：创建分区](lesson-10-create-partitions.md)。  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a>使用默认透视和 Internet 销售透视进行浏览  
 在第一批任务中，您将使用默认透视（包含所有模型对象）和您在第 8 课“创建透视”中创建的“Internet Sales”透视来浏览您的模型。 “Internet Sales”透视将排除 Customer 表对象。  
  
#### <a name="to-browse-by-using-the-default-perspective"></a>使用默认透视进行浏览  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，单击 **“模型”** 菜单，然后单击 **“在 Excel 中分析”**。  
  
2.  在“在 Excel 中分析”对话框中，单击“确定”。********  
  
     Excel 将打开一个新的工作簿。 将使用当前用户帐户创建一个数据源连接，默认透视将用于定义可查看字段。 数据透视表将自动添加到工作表中。  
  
3.  在 Excel 的 "**数据透视表字段列表**" 中，请注意，将显示 "**日期**" 和 " **internet 销售**" 度量值，以及 "**客户**"、"**日期**"、"**地域**"、"**产品**"、"产品**类别**"、"**产品子类别**" 和 " **Internet 销售**" 表，其中  
  
4.  关闭 Excel 且不保存工作簿。  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a>使用 Internet 销售透视进行浏览  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，单击 **“模型”** 菜单，然后单击 **“在 Excel 中分析”**。  
  
2.  在“在 Excel 中分析”对话框中，使“当前 Windows 用户”保持选中状态，在“透视”下拉列表框中选择“Internet 销售”，并单击“确定”。******************** Excel 将打开。  
  
3.  在 Excel 的“数据透视表字段列表”**** 中，请注意 Customer 表已从字段列表中排除。  
  
## <a name="browse-using-roles"></a>使用角色进行浏览  
 角色是任何表格模型中不可或缺的一部分。 一个角色都没有（用户可以作为成员添加到这些角色），用户将不能使用您的模型访问和分析数据。 “在 Excel 中分析”功能为您提供测试所定义的角色的方法。  
  
#### <a name="to-browse-by-using-the-internet-sales-manager-user-role"></a>使用“Internet Sales Manager”用户角色进行浏览  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，单击 **“模型”** 菜单，然后单击 **“在 Excel 中分析”**。  
  
2.  在“在 Excel 中分析”**** 对话框的“指定要用于连接到模型的用户名或角色”**** 中，选中“角色”****，然后在下拉列表框中，选中 **Internet Sales Manager**，然后单击“确定”****。  
  
     Excel 将打开一个新的工作簿。 将自动创建一个数据透视表。 数据透视表字段列表包含您的新模型中提供的所有数据字段。  
  
## <a name="next-steps"></a>后续步骤  
 要继续学习本教程，请转到下一课： [第 14 课：部署](lesson-13-deploy.md)。  
  
  
