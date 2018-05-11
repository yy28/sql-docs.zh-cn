---
title: Analysis Services 教程课 11： 创建角色 |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfiles"
ms.openlocfilehash: 3a41b55afcbc5ac3c8bb3e87a64708f6806615df
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="create-roles"></a>创建角色

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，你将创建角色。 角色提供通过限制对仅这些角色成员的用户访问的模型数据库对象和数据安全。 每个角色都使用单个权限进行定义：“无”、“读取”、“读取和处理”、“处理”或“管理员”。 可以通过使用角色管理器中创作模型期间定义角色。 部署某一模型后，您可以通过使用 SQL Server Management Studio (SSMS) 来管理角色。 若要了解详细信息，请参阅[角色](../tabular-models/roles-ssas-tabular.md)。
  
> [!NOTE]  
> 创建角色对于完成本教程不是必需的。 默认情况下，你当前登录时所用的帐户对模型具有管理员权限。 但是，若要使用的报表客户端浏览你的组织中其他用户，必须创建至少一个角色具有读取权限并将这些用户添加为成员。  
  
创建三个角色：  
  
-   **销售经理**– 此角色可以包括在你想要对所有模型对象和数据具有读取权限的组织中的用户。  
  
-   **销售分析人员美国**– 此角色可以的组织想仅要能够浏览在美国国内的销售与相关的数据中包括的用户。 为此角色，你使用 DAX 公式来定义*行筛选器*，限制要浏览仅适用于美国境内数据成员。  
  
-   **管理员**– 此角色可以包括你想要具有管理员权限，这允许不受限制的访问和对模型数据库执行管理任务的权限的用户。  
  
因为贵组织中的 Windows 用户和组帐户是唯一的，所以您可以从您的特定组织向成员添加帐户。 但是，对于本教程，您还可以将成员保留为空。 课程 12 更高版本中测试每个角色的效果： 在 Excel 中分析。  
  
学完本课的估计时间： **15 分钟**  
  
## <a name="prerequisites"></a>必要條件  

本文摘自表格建模教程中，应按顺序完成。 之前在本课程中执行任务，你应完成上一课：[课 10： 创建分区](../tutorial-tabular-1400/as-lesson-10-create-partitions.md)。  
  
## <a name="create-roles"></a>创建角色  
  
#### <a name="to-create-a-sales-manager-user-role"></a>创建 Sales Manager 用户角色  
  
1.  在表格模型资源管理器，右键单击**角色** > **角色**。  
  
2.  在角色管理器中，单击**新建**。  
  
3.  单击新的角色，然后在**名称**列中，重命名该角色向**销售经理**。  
  
4.  在“权限”列中，单击下拉列表，然后选择“读取”权限。 

    ![as-lesson11-new-role](../tutorial-tabular-1400/media/as-lesson11-new-role.png) 
  
5.  可选： 单击**成员**选项卡上，并依次**添加**。 在“选择用户或组”对话框中，输入要包括在角色中的来自组织的 Windows 用户或组。  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>创建 Sales Analyst US 用户角色  
  
1.  在角色管理器中，单击**新建**。    
  
2.  重命名该角色向**销售分析师美国**。  
  
3.  为此角色**读取**权限。  
  
4.  单击行筛选器选项卡，然后为**DimGeography**表仅在 DAX 筛选器列中，键入以下公式：  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    行筛选器公式必须解析为布尔 (TRUE/FALSE) 值。 此公式中，使用您所指定的国家 / 地区代码值"美国"的行对用户可见。  
    ![作为 lesson11-角色-筛选器](../tutorial-tabular-1400/media/as-lesson11-role-filter.png) 
  
6.  可选： 单击**成员**选项卡上，并依次**添加**。 在“选择用户或组”对话框中，输入要包括在角色中的来自组织的 Windows 用户或组。  
  
#### <a name="to-create-an-administrator-user-role"></a>若要创建的管理员用户角色  
  
1.  单击 **“新建”**。  
  
2.  重命名该角色向**管理员**。  
  
3.  为此角色**管理员**权限。  
  
4.  可选： 单击**成员**选项卡上，并依次**添加**。 在“选择用户或组”对话框中，输入要包括在角色中的来自组织的 Windows 用户或组。 
  
  
## <a name="whats-next"></a>下一步是什么？

[课程 12: 在 Excel 中分析](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)。

  
  
