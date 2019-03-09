---
title: Analysis Services 教程第 11 课：创建角色 |Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfiles"
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: e75f1b9f838b09bbe4ab219aacd2616e04328238
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685454"
---
# <a name="create-roles"></a>创建角色

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

在本课程中，将创建角色。 角色通过限制访问权限仅这些用户属于角色成员提供模型数据库对象和数据安全性。 每个角色定义有单一权限：无、 读取、 读取和进程、 进程或管理员。 可以通过使用角色管理器中创作模型期间定义角色。 在部署某一模型后，可以通过使用 SQL Server Management Studio (SSMS) 来管理角色。 若要了解详细信息，请参阅[角色](../tabular-models/roles-ssas-tabular.md)。
  
> [!NOTE]  
> 创建角色对于完成本教程不是必需的。 默认情况下，你当前登录时所用的帐户具有管理员权限的模型。 但是，若要浏览使用报告客户端在组织中其他用户，必须创建至少一个角色具有读取权限并将这些用户添加为成员。  
  
创建三个角色：  
  
-   **销售经理**-此角色可以包括在你想要对所有模型对象和数据具有读取权限的组织中的用户。  
  
-   **Sales Analyst US** -此角色可以包括希望只是为了能够浏览与在美国的销售相关的数据在组织中的用户。 对于此角色，您使用 DAX 公式来定义*行筛选器*，限制要浏览仅对美国的数据成员。  
  
-   **管理员**-此角色可以包括你想要具有管理员权限，允许无限制访问权限和对模型数据库执行管理任务的权限的用户。  
  
因为贵组织中的 Windows 用户和组帐户是唯一的，所以您可以从您的特定组织向成员添加帐户。 但是，对于本教程，您还可以将成员保留为空。 更高版本在第 12 课中测试每个角色的效果：在 Excel 中分析。  
  
学完本课的预计时间：**15 分钟**  
  
## <a name="prerequisites"></a>先决条件  

本文是表格建模教程应按顺序完成的一部分。 执行任务之前在本课程中，您应当已完成上一课：[第 10 课：创建分区](../tutorial-tabular-1400/as-lesson-10-create-partitions.md)。  
  
## <a name="create-roles"></a>创建角色  
  
#### <a name="to-create-a-sales-manager-user-role"></a>创建 Sales Manager 用户角色  
  
1.  在表格模型资源管理器，右键单击**角色** > **角色**。  
  
2.  在角色管理器中，单击**新建**。  
  
3.  单击新角色，然后在**名称**列中，重命名为**销售经理**。  
  
4.  在“权限”列中，单击下拉列表，然后选择“读取”权限。 

    ![as-lesson11-new-role](../tutorial-tabular-1400/media/as-lesson11-new-role.png) 
  
5.  可选:单击**成员**选项卡，然后依次**添加**。 在“选择用户或组”对话框中，输入要包括在角色中的来自组织的 Windows 用户或组。  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>创建 Sales Analyst US 用户角色  
  
1.  在角色管理器中，单击**新建**。    
  
2.  重命名为**Sales Analyst US**。  
  
3.  向此角色授予**读取**权限。  
  
4.  单击行筛选器选项卡，然后**DimGeography**表仅在 DAX 筛选器列中，键入以下公式：  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    行筛选器公式必须解析为布尔 (TRUE/FALSE) 值。 通过此公式中，指定的国家/地区区域代码值为"US"行对用户可见。  
    ![as-lesson11-role-filter](../tutorial-tabular-1400/media/as-lesson11-role-filter.png) 
  
6.  可选:单击**成员**选项卡，然后依次**添加**。 在“选择用户或组”对话框中，输入要包括在角色中的来自组织的 Windows 用户或组。  
  
#### <a name="to-create-an-administrator-user-role"></a>若要创建的管理员用户角色  
  
1.  单击 **“新建”**。  
  
2.  重命名为**管理员**。  
  
3.  向此角色授予**管理员**权限。  
  
4.  可选:单击**成员**选项卡，然后依次**添加**。 在“选择用户或组”对话框中，输入要包括在角色中的来自组织的 Windows 用户或组。 
  
  
## <a name="whats-next"></a>下一步是什么？

[第 12 课：在 Excel 中分析](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md)。

  
  
