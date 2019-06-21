---
title: 角色 (SSAS 表格) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e547382a-c064-4bc6-818c-5127890af334
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd4e54a0099e459d52577de23acc5c4f2989edc5
ms.sourcegitcommit: 0818f6cc435519699866db07c49133488af323f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284861"
---
# <a name="roles-ssas-tabular"></a>角色（SSAS 表格）
  在表格模型中，角色定义模型的成员权限。 每个角色都包含成员（按 Windows 用户名或按 Windows 组）和权限（读取、处理、管理员）。 该角色的成员可按照角色权限的定义对模型执行操作。 使用读取权限定义的角色也可以通过使用行级别筛选器在行级别提供附加的安全性。  
  
> [!IMPORTANT]  
>  为使用户通过使用报表或数据分析客户端应用程序连接到已部署的模型，您必须创建这些用户是其成员的至少一个角色并且该角色至少具有读取权限。  
  
 本主题中的信息面向通过使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的“角色管理器”对话框定义角色的表格模型作者。 在模型创作期间定义的角色适用于模型工作区数据库。 在已部署某一模型数据库后，模型数据库管理员可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 管理（添加、编辑、删除）角色成员。 若要了解如何在已部署的数据库中管理角色的成员，请参阅[表格模型角色（SSAS 表格）](tabular-model-roles-ssas-tabular.md)。  
  
 [表格建模（Adventure Works 教程）](../tabular-modeling-adventure-works-tutorial.md)包括有关如何使用此功能的其他信息和课程。  
  
 本主题的内容：  
  
-   [了解角色](#bkmk_underst)  
  
-   [Permissions](#bkmk_permissions)  
  
-   [行筛选器](#bkmk_rowfliters)  
  
-   [测试角色](#bkmk_testroles)  
  
-   [相关任务](#bkmk_rt)  
  
##  <a name="bkmk_underst"></a> 了解角色  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中使用角色来管理 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和数据的安全性。 在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中有两种类型的角色：  
  
-   服务器角色，它是一个固定角色，用于提供对 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例的管理员访问权限。  
  
-   数据库角色，这些角色由模型作者和管理员定义，用于控制非管理员用户对模型数据库和数据的访问权限。  
  
 为表格模型定义的角色是数据库角色。 也就是说，角色包含由 Windows 用户或组构成的成员，这些用户或组具有定义这些成员可对模型数据库执行的操作的特定权限。 数据库角色作为数据库中的单独对象进行创建，并且仅应用于在其中创建该角色的数据库。 Windows 用户和/或 Windows 组包含在模型作者默认情况下按其对工作区数据库服务器具有管理员权限的角色中；对于已部署的模型，将按管理员。  
  
 可以进一步使用行筛选器定义表格模型中的角色。 行筛选器使用 DAX 表达式定义表中的行，以及许多方向中用户可以查询的任何相关行。 只能为“读取”和“读取和处理”权限定义使用 DAX 表达式的行筛选器。 有关详细信息，请参阅本主题后面的 [行筛选器](#bkmk_rowfliters) 。  
  
 默认情况下，当您创建某一新的表格模型项目时，该模型项目不具有任何角色。 可以使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中的“角色管理器”对话框定义角色。 在创作模型期间定义角色后，这些角色将应用于模型工作区数据库。 在部署模型时，相同的角色将应用于已部署的模型。 在部署了某一模型后，服务器角色的成员（[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 管理员）和数据库管理员可以通过使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]管理与该模型相关联的角色以及与各个角色相关联的成员。  
  
> [!NOTE]  
>  为 DirectQuery 模式配置的模型定义的角色无法使用行筛选器，但是，为每个角色定义的权限将适用。  
  
##  <a name="bkmk_permissions"></a> Permissions  
 每个角色都具有单个定义的数据库权限（合并的“读取和处理”权限除外）。 默认情况下，新角色将具有“无”权限。 也就是说，一旦将成员添加到具有“无”权限的角色，除非授予其他权限，否则，这些成员将无法修改数据库、运行处理操作、查询数据或查看数据库。  
  
 Windows 组或用户可以是任何数目的角色的成员，每个角色具有不同的权限。 在某一用户是多个角色的成员时，为每个角色定义的权限将累积。 例如，如果某个用户是具有“读取”权限的角色的成员，并且还是具有“无”权限的角色的成员，则该用户将具有“读取”权限。  
  
 每个角色都可以定义下列权限之一：  
  
|权限|Description|使用 DAX 进行行筛选|  
|-----------------|-----------------|----------------------------|  
|None|成员无法对模型数据库架构进行任何修改，也无法查询数据。|不应用行筛选器。 此角色中的用户无法看见数据|  
|读取|允许成员查询数据（基于行筛选器），但是无法看到 SSMS 中的模型数据库，无法更改模型数据库架构，并且用户无法处理模型。|应用行筛选器。 用户仅能看见在行筛选器 DAX 公式中指定的数据。|  
|读取和处理|允许成员查询数据（基于行级别筛选器）并通过运行包含处理命令的脚本或包来运行处理操作，但无法对数据库进行任何更改。 无法在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中查看模型数据库。|应用行筛选器。 仅能查询在行筛选器 DAX 公式中指定的数据。|  
|处理|成员可以通过运行包含处理命令的脚本或包来运行处理操作。 不能修改模型数据库架构。 无法查询数据。 无法在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中查询模型数据库。|不应用行筛选器。 此角色中没有可查询的数据|  
|管理员|成员可以对模型架构进行任何修改并可以查询模型设计器、报表客户端和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的所有数据。|不应用行筛选器。 此角色中的所有数据均可查询。|  
  
##  <a name="bkmk_rowfliters"></a> 行筛选器  
 行筛选器定义表中可供特定角色的成员进行查询的行。 通过使用 DAX 公式为模型中的每个表定义行筛选器。  
  
 只能为具有“读取”和“读取和处理”权限的角色定义行筛选器。 默认情况下，如果没有为某一特定表定义行筛选器，则具有“读取”和“读取和处理”权限的角色的成员将能够查询表中的所有行，除非交叉筛选应用于其他表。  
  
 一旦为特定表定义了行筛选器后，求值结果必须为 TRUE/FALSE 值的 DAX 公式将定义可供该特定角色的成员进行查询的行。 未包含在 DAX 公式中的行将不可查询。 例如，对于 Sales 角色的成员，Customers 表的以下行筛选器表达式中， *= Customers [Country] ="USA"*，Sales 角色的成员将只能查看美国境内的客户。  
  
 行筛选器应用于指定的行以及相关行。 如果表具有多个关系，则筛选器将安全性应用于处于活动状态的关系。 行筛选器将与为相关表定义的其他行筛选器相交，例如：  
  
|表|DAX 表达式|  
|-----------|--------------------|  
|地区|=Region[Country]="USA"|  
|ProductCategory|=ProductCategory[Name]="Bicycles"|  
|事务|=Transactions[Year]=2008|  
  
 这些权限对于 Transactions 表的净效果是，将允许成员查询客户位于 USA、产品类别是自行车并且年份是 2008 的数据行。 用户将无法查询 USA 之外的任何事务、不是自行车的任何事务或者不在 2008 年发生的任何事务，除非用户是授予了这些权限的其他角色。  
  
 可使用筛选器 =FALSE() 来拒绝对整个表所有行的访问。  
  
### <a name="dynamic-security"></a>动态安全性  
 动态安全性提供了一种基于当前登录用户的用户名或从连接字符串返回的 CustomData 属性定义行级别安全性的方式。 为了实现动态安全性，您必须在模型中包含一个具有用户登录名（Windows 用户名）值的表以及一个可用于定义特定权限的字段；例如，一个具有登录 ID (domain\username) 的 dimEmployees 表以及一个针对每个员工的部门值。  
  
 为了实现动态安全性，您可以使用以下函数作为 DAX 公式的一部分来返回当前登录用户的用户名，或者返回连接字符串中的 CustomData 属性：  
  
|函数|Description|  
|--------------|-----------------|  
|[USERNAME 函数&#40;DAX&#41;](/dax/username-function-dax)|返回当前登录用户的 domain\username。|  
|[CUSTOMDATA 函数&#40;DAX&#41;](/dax/customdata-function-dax)|返回连接字符串中的 CustomData 属性。|  
  
 您可以使用 LOOKUPVALUE 函数返回某一列的值，在该列中，Windows 用户名与 USERNAME 函数返回的用户名或 CustomData 函数返回的字符串相同。 然后，可以限制查询，只显示 LOOKUPVALUE 返回的值与相同或相关表中的值匹配的行。  
  
 例如，使用以下公式：  
  
 `='dimDepartmentGroup'[DepartmentGroupId]=LOOKUPVALUE('dimEmployees'[DepartmentGroupId], 'dimEmployees'[LoginId], USERNAME(), 'dimEmployees'[LoginId], 'dimDepartmentGroup'[DepartmentGroupId])`  
  
 LOOKUPVALUE 函数返回其 dimEmployees[LoginId] 与 USERNAME 返回的当前登录用户的 LoginID 相同的 dimEmployees[DepartmentId] 列的值，并且 dimEmployees[DepartmentId] 的值与 dimDepartmentGroup[DepartmentId] 的值相同。 然后，使用 LOOKUPVALUE 所返回的 DepartmentId 中的值来限制在 dimDepartment 表中查询的行以及通过 DepartmentId 关联的任何表。 将只返回其 DepartmentId 也在 LOOKUPVALUE 函数返回的 DepartmentId 的值中的行。  
  
 **dimEmployees**  
  
|LastName|FirstName|LoginID|DepartmentName|DepartmentId|  
|--------------|---------------|-------------|--------------------|------------------|  
|Brown|Kevin|Adventure-works\kevin0|Marketing|7|  
|Bradley|David|Adventure-works\david0|Marketing|7|  
|Dobney|JoLynn|Adventure-works\JoLynn0|Production|4|  
|Baretto DeMattos|Paula|Adventure-works\Paula0|Human Resources|2|  
  
 **dimDepartment**  
  
|DepartmentId|DepartmentName|  
|------------------|--------------------|  
|1|企业|  
|2|一般行政和管理|  
|3|库存管理|  
|4|生产|  
|5|质量保证|  
|6|研究和开发|  
|7|销售和营销|  
  
##  <a name="bkmk_testroles"></a> 测试角色  
 在创作模型项目时，可以使用“在 Excel 中分析”功能来测试已定义的角色的效用。 从模型设计器中的 **“模型”** 菜单中，当您单击 **“在 Excel 中分析”** 时，在打开 Excel 之前，将会出现 **“选择凭据和透视”** 对话框。 在此对话框中，您可以指定当前用户名、其他用户名、角色和一个用于连接作为数据源的工作区模型的透视。 有关详细信息，请参阅本主题后面的 [在 Excel 中分析（SSAS 表格）](analyze-in-excel-ssas-tabular.md)中的“角色管理器”对话框定义角色的表格模型作者。  
  
##  <a name="bkmk_rt"></a> 相关任务  
  
|主题|Description|  
|-----------|-----------------|  
|[创建和管理角色（SSAS 表格）](create-and-manage-roles-ssas-tabular.md)|本主题中的任务说明如何使用 **“角色管理器”** 对话框来创建和管理角色。|  
  
## <a name="see-also"></a>请参阅  
 [透视表（SSAS 表格）](perspectives-ssas-tabular.md)   
 [在 Excel 中分析（SSAS 表格）](analyze-in-excel-ssas-tabular.md)   
 [USERNAME 函数&#40;DAX&#41;](/dax/username-function-dax)   
 [LOOKUPVALUE 函数&#40;DAX&#41;](/dax/lookupvalue-function-dax)   
 [CUSTOMDATA 函数&#40;DAX&#41;](/dax/customdata-function-dax)  
  
  
