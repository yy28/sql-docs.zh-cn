---
title: 使用 SSMS 管理 Analysis Services 表格模型角色 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 22fd8242de50f73eee634d1bc6bc3fcf5e887f0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162804"
---
# <a name="manage-roles-by-using-ssms"></a>使用 SSMS 管理角色 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  对于部署的表格模型，可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]创建、编辑和管理角色。  
  
 本主题中的任务：  
  
-   [创建新角色](#bkmk_new_role)  
  
-   [复制角色](#bkmk_copy_role)  
  
-   [编辑角色](#bkmk_edit_role)  
  
-   [删除角色](#bkmk_deletet_role)  
  
> [!CAUTION]  
>  在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中通过角色管理器使用已定义的角色重新部署表格模型项目，将覆盖已部署的表格模型中定义的角色。  
  
> [!CAUTION]  
>  如果在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中打开模型项目时使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 来管理表格模型工作区数据库，可能会导致 Model.bim 文件损坏。 在创建和管理表格模型工作区数据库的角色时，请使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中的角色管理器。  
  
###  <a name="bkmk_new_role"></a> 创建新角色  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，展开要为其创建新角色的表格模型数据库，右键单击 **“角色”** ，然后单击 **“新建角色”** 。  
  
2.  在 **“创建角色”** 对话框的“选择页”窗口中，单击 **“常规”** 。  
  
3.  在常规设置窗口的 **“名称”** 字段中，键入角色的名称。  
  
     默认情况下，对于每个新建角色，默认角色的名称将为递增式编号。 建议您键入明确标识成员类型的名称，例如财务经理或人力资源专员。  
  
4.  在 **“为此角色设置数据库权限”** 中，选择以下权限选项之一：  
  
    |权限|描述|  
    |----------------|-----------------|  
    |**完全控制(管理员)**|成员可以对模型架构进行修改并可以查看所有数据。|  
    |**处理数据库**|成员可以运行“处理”和“全部处理”操作。 不能修改模型架构且不能查看数据。|  
    |**读取**|允许成员查看数据（基于行筛选器），但不能对模型架构进行任何更改。|  
  
5.  在 **“创建角色”** 对话框的“选择页”窗口中，单击 **“成员身份”** 。  
  
6.  在“成员身份设置”窗口中单击 **“添加”** ，然后在 **“选择用户或组”** 对话框中，添加要作为成员添加的 Windows 用户或组。  
  
7.  如果您创建的角色已具有“读取”权限，则可以使用 DAX 公式为任意表添加行筛选器。 若要在中添加行筛选器**角色属性- \<rolename >** 对话框中，在**选择页**，单击**行筛选器**。  
  
8.  在行筛选器窗口中，选择一个表，然后单击**DAX 筛选器**字段中，然后在**DAX 筛选器- \<tablename >** 字段中键入 DAX 公式。  
  
    > [!NOTE]  
    >  DAX 筛选器-\<表名称 > 字段不包含自动完成查询编辑器或插入函数功能。 若要在写入 DAX 公式时使用自动完成功能，必须在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中使用 DAX 公式编辑器。  
  
9. 单击 **“确定”** 保存角色。  
  
###  <a name="bkmk_copy_role"></a> 复制角色  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，展开包含要复制的角色的表格模型数据库，展开 **“角色”** ，右键单击该角色，然后单击 **“复制”** 。  
  
###  <a name="bkmk_edit_role"></a> 编辑角色  
  
-   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，展开包含要编辑的角色的表格模型数据库，展开 **“角色”** ，右键单击该角色，然后单击 **“属性”** 。  
  
     在中**角色属性** \<rolename > 对话框中，可以更改权限、 添加或删除成员，以及添加/编辑行筛选器。  
  
###  <a name="bkmk_deletet_role"></a> 删除角色  
  
-   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，展开包含要删除的角色的表格模型数据库，展开 **“角色”** ，右键单击该角色，然后单击 **“删除”** 。  
  
## <a name="see-also"></a>请参阅  
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
