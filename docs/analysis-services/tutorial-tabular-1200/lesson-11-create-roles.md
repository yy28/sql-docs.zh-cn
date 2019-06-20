---
title: 第 12 课：创建角色 |Microsoft Docs
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d6ba289eed3e700034ed73d3f45ca3e0d963e385
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65404479"
---
# <a name="lesson-11-create-roles"></a>第 11 课：创建角色
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

在本课中，您将创建角色。 角色通过只限作为角色成员的那些 Windows 用户进行访问，提供模型数据库对象和数据的安全性。 每个角色定义有单一权限：无、 读取、 读取和进程、 进程或管理员。 可以通过使用角色管理器中创作模型期间定义角色。 在部署模型后，可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]管理角色。 若要了解详细信息，请参阅[角色](../tabular-models/roles-ssas-tabular.md)。  
  
> [!NOTE]  
> 创建角色对于完成本教程不是必需的。 默认情况下，您当前登录的帐户对于模型将具有管理员权限。 但是，若要允许组织使用报告客户端浏览该模型中的其他用户，必须创建至少一个角色具有读取权限并将这些用户添加为成员。  
  
您将创建三个角色：  
  
-   **销售经理**-此角色可以包括在你想要对所有模型对象和数据具有读取权限的组织中的用户。  
  
-   **Sales Analyst US** -此角色可以包括希望只是为了能够浏览与在美国的销售相关的数据在组织中的用户。 对于此角色，使用 DAX 公式来定义“行筛选器”，该筛选器将成员限制为只能浏览针对美国的数据。  
  
-   **管理员**-此角色可以包括你想要具有管理员权限，允许无限制访问权限和对模型数据库执行管理任务的权限的用户。  
  
因为贵组织中的 Windows 用户和组帐户是唯一的，所以您可以从您的特定组织向成员添加帐户。 但是，对于本教程，您还可以将成员保留为空。 您仍能够测试每个角色的影响，更高版本中第 12 课：在 Excel 中分析。  
  
估计的时间才能完成本课程中：**15 分钟**  
  
## <a name="prerequisites"></a>先决条件  
本主题是表格建模教程的一部分，该教程应按顺序学习。 执行任务之前在本课程中，您应当已完成上一课：[第 10 课：创建分区](lesson-10-create-partitions.md)。  
  
## <a name="create-roles"></a>创建角色  
  
#### <a name="to-create-a-sales-manager-user-role"></a>创建 Sales Manager 用户角色  
  
1.  在表格模型资源管理器，右键单击**角色** > **角色**。  
  
2.  在角色管理器中，单击**新建**。  
  
3.  单击新角色，然后在**名称**列中，重命名为**销售经理**。  
  
4.  在“权限”列中，单击下拉列表，然后选择“读取”权限。 

    ![as-tabular-lesson11-new-role](media/as-tabular-lesson11-new-role.png) 
  
5.  可选：单击**成员**选项卡，然后依次**添加**。 在“选择用户或组”对话框中，输入要包括在角色中的来自组织的 Windows 用户或组。  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>创建 Sales Analyst US 用户角色  
  
1.  在角色管理器中，单击**新建**。    
  
2.  重命名为**Sales Analyst US**。  
  
3.  向此角色授予**读取**权限。  
  
4.  单击行筛选器选项卡，然后对于**DimGeography**表仅在 DAX 筛选器列中，键入以下公式：  
  
    ```
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    行筛选器公式必须解析为布尔 (TRUE/FALSE) 值。 通过此公式中，指定的国家/地区区域代码值为"US"行，对用户可见。  
    ![as-tabular-lesson11-role-filter](media/as-tabular-lesson11-role-filter.png) 
  
6.  可选：单击“成员”选项卡，然后单击“添加”。 在“选择用户或组”对话框中，输入要包括在角色中的来自组织的 Windows 用户或组。  
  
#### <a name="to-create-an-administrator-user-role"></a>若要创建的管理员用户角色  
  
1.  单击 **“新建”**。  
  
2.  重命名为**管理员**。  
  
3.  向此角色授予**管理员**权限。  
  
4.  可选：单击“成员”选项卡，然后单击“添加”。 在“选择用户或组”对话框中，输入要包括在角色中的来自组织的 Windows 用户或组。 
  
  
## <a name="whats-next"></a>下一步是什么？
请转到下一课：[第 12 课：在 Excel 中分析](lesson-12-analyze-in-excel.md)。

  
  
