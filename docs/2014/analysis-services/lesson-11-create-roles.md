---
title: 第 12 课： 创建角色 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 984face4-00fc-46d3-8ae1-9755bf737bdf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d3ca1e013ede0e8bd40c1ce5af36d44ea45122d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164077"
---
# <a name="lesson-12-create-roles"></a>第 12 课：创建角色
  在本课中，您将创建角色。 角色通过只限作为角色成员的那些 Windows 用户进行访问，提供模型数据库对象和数据的安全性。 每个角色都使用单个权限进行定义：“无”、“读取”、“读取和处理”、“处理”或“管理员”。 通过使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中的“角色管理器”对话框，可在模型创作期间定义角色。 在部署模型后，可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 管理角色。 若要了解详细信息，请参阅[角色（SSAS 表格）](tabular-models/roles-ssas-tabular.md)。  
  
> [!NOTE]  
>  创建角色对于完成本教程不是必需的。 默认情况下，您当前登录的帐户对于模型将具有管理员权限。 但是，为了让贵组织中的其他用户能够通过报表客户端应用程序浏览模型，您必须至少创建一个具有“读取”权限的角色，并将这些用户添加为成员。  
  
 您将创建三个角色：  
  
-   Sales Manager - 此角色可以包含贵组织中您希望其对所有模型对象和数据具有“读取”权限的用户。  
  
-   Sales Analyst US - 此角色可以包含贵组织中您希望其只能浏览与 US（美国）的销售有关的数据的用户。 对于此角色，使用 DAX 公式来定义“行筛选器”，该筛选器将成员限制为只能浏览针对美国的数据。  
  
-   Administrator - 此角色包含您希望其具有管理员权限的用户，管理员权限可让用户具有不受限制的访问权限，从而对模型数据库执行管理任务。  
  
 因为贵组织中的 Windows 用户和组帐户是唯一的，所以您可以从您的特定组织向成员添加帐户。 但是，对于本教程，您还可以将成员保留为空。 在稍后的第 12 课“在 Excel 中分析”中，您将仍可以测试每个角色的影响。  
  
 学完本课的估计时间： **15 分钟**  
  
## <a name="prerequisites"></a>必要條件  
 本主题是表格建模教程的一部分，该教程应按顺序学习。 在执行本课程中的任务之前，须已完成上一课： [第 11 课：创建分区](lesson-10-create-partitions.md)。  
  
## <a name="create-roles"></a>创建角色  
  
#### <a name="to-create-a-sales-manager-user-role"></a>创建 Sales Manager 用户角色  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，单击“模型”菜单，然后单击“角色”。  
  
2.  在 **“角色管理器”** 对话框中，单击 **“新建”**。  
  
     一个具有“无”权限的新角色将添加到列表中。  
  
3.  单击新角色，然后在**名称**列中，重命名为`Internet Sales Manager`。  
  
4.  在“权限”列中，单击下拉列表，然后选择“读取”权限。  
  
5.  可选：单击“成员”选项卡，然后单击“添加”。  
  
6.  在“选择用户或组”对话框中，输入要包括在角色中的来自组织的 Windows 用户或组。  
  
7.  确认你的选择，然后单击“确定”。  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>创建 Sales Analyst US 用户角色  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中，单击“模型”菜单，然后单击“角色”。  
  
2.  在 **“角色管理器”** 对话框中，单击 **“新建”**。  
  
     一个具有“无”权限的新角色将添加到列表中。  
  
3.  单击新角色，然后在**名称**列中，重命名为`Internet Sales US`。  
  
4.  在“权限”列中，单击下拉列表，然后选择“读取”权限。  
  
5.  单击“行筛选器”选项卡，然后只针对 **Geography** 表，在“DAX 筛选器”列中键入以下公式：  
  
     `=Geography[Country Region Code] = "US"`  
  
     行筛选器公式必须解析为布尔 (TRUE/FALSE) 值。 利用此公式，您可指定只有 Country Region Code 值为“US”的行才对用户可见。  
  
     在您完成公式的建立后，按 Enter。  
  
6.  可选：单击“成员”选项卡，然后单击“添加”。  
  
7.  在“选择用户或组”对话框中，输入要包括在角色中的来自组织的 Windows 用户或组。  
  
8.  确认你的选择，然后单击“确定”。  
  
#### <a name="to-create-an-administrator-role"></a>创建 Administrator 角色  
  
1.  在 **“角色管理器”** 对话框中，单击 **“新建”**。  
  
2.  单击新角色，然后在**名称**列中，重命名为`Internet Sales Administrator`。  
  
3.  在“权限”列中，单击下拉列表，然后选择“管理员”权限。  
  
4.  单击“成员”选项卡，然后单击“添加”。  
  
5.  可选：在“选择用户或组”对话框中，输入要包括在角色中的来自组织的 Windows 用户或组。  
  
6.  确认你的选择，然后单击“确定”。  
  
## <a name="next-steps"></a>后续步骤  
 若要继续学习本教程，请转到下一课：课程： [第 13 课：在 Excel 中进行分析](lesson-12-analyze-in-excel.md)。  
  
  
