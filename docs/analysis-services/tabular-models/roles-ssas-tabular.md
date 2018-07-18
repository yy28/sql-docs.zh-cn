---
title: 角色 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3ebefae10d3c1cd4791cc38fd5b9d30e5e29838a
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2018
ms.locfileid: "38981529"
---
# <a name="roles"></a>角色
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  在表格模型中，角色定义模型的成员权限。 该角色的成员可按照角色权限的定义对模型执行操作。 使用读取权限定义的角色也可以通过使用行级别筛选器在行级别提供附加的安全性。 
  
 对于 SQL Server Analysis Services，角色包含用户的成员，按 Windows 用户名或按 Windows 组和权限 （读取、 过程、 管理员）。 对于 Azure Analysis Services，用户必须位于你的 Azure Active Directory 和用户名，并指定组必须是组织的电子邮件地址或 UPN。 
  
> [!IMPORTANT]  
>  对于用户通过使用报表客户端应用程序连接到已部署的模型，您必须创建至少一个角色至少读取到的这些用户是成员的权限。  
  
 本主题中的信息适用于表格模型作者使用 SSDT 中的角色管理器对话框定义角色。 在模型创作期间定义的角色适用于模型工作区数据库。 已部署的模型数据库后，模型数据库管理员可以管理 （添加、 编辑、 删除） 通过使用 SSMS 的角色成员。 若要了解如何管理已部署的数据库中的角色的成员，请参阅[表格模型角色](../../analysis-services/tabular-models/tabular-model-roles-ssas-tabular.md)。  
  
##  <a name="bkmk_underst"></a> Understanding roles  
 Analysis Services 中使用角色来管理模型数据访问。 有两种类型的角色：  
  
-   服务器角色，提供管理员访问权限的 Analysis Services 服务器实例的固定角色。  
  
-   数据库角色，这些角色由模型作者和管理员定义，用于控制非管理员用户对模型数据库和数据的访问权限。  
  
 为表格模型定义的角色是数据库角色。 也就是说，角色包含构成用户的成员或拥有特定权限来定义操作，这些成员的组可能需要对模型数据库。 数据库角色作为数据库中的单独对象进行创建，并且仅应用于在其中创建该角色的数据库。 用户和组的角色中包含由模型作者，后者默认情况下，在工作区数据库服务器; 上具有管理员权限已部署的模型，由管理员。  
  
 可以进一步使用行筛选器定义表格模型中的角色。 行筛选器使用 DAX 表达式定义表中的行，以及许多方向中用户可以查询的任何相关行。 只能为“读取”和“读取和处理”权限定义使用 DAX 表达式的行筛选器。 若要了解详细信息，请参阅[行筛选器](#bkmk_rowfliters)本主题中更高版本。  
  
 默认情况下，当您创建某一新的表格模型项目时，该模型项目不具有任何角色。 可以通过使用 SSDT 中的角色管理器对话框定义角色。 在创作模型期间定义角色后，这些角色将应用于模型工作区数据库。 在部署模型时，相同的角色将应用于已部署的模型。 在部署某一模型后，服务器角色 （[Analysis Services 管理员） 和数据库管理员的成员可以管理与模型相关联的角色和使用 SSMS 来关联与每个角色的成员。  
  
##  <a name="bkmk_permissions"></a> Permissions  
 每个角色都具有单个定义的数据库权限（合并的“读取和处理”权限除外）。 默认情况下，新角色将具有“无”权限。 也就是说，一旦将成员添加到具有“无”权限的角色，除非授予其他权限，否则，这些成员将无法修改数据库、运行处理操作、查询数据或查看数据库。  
  
 组或用户可以是任意数量的角色，具有不同的权限的每个角色的成员。 在某一用户是多个角色的成员时，为每个角色定义的权限将累积。 例如，如果某个用户是具有“读取”权限的角色的成员，并且还是具有“无”权限的角色的成员，则该用户将具有“读取”权限。  
  
 每个角色都可以定义下列权限之一：  
  
|权限|Description|使用 DAX 进行行筛选|  
|-----------------|-----------------|----------------------------|  
|InclusionThresholdSetting|成员无法对模型数据库架构进行任何修改，也无法查询数据。|不应用行筛选器。 此角色中的用户无法看见数据|  
|读取|允许成员查询数据（基于行筛选器），但是无法看到 SSMS 中的模型数据库，无法更改模型数据库架构，并且用户无法处理模型。|应用行筛选器。 用户仅能看见在行筛选器 DAX 公式中指定的数据。|  
|读取和处理|允许成员查询数据（基于行级别筛选器）并通过运行包含处理命令的脚本或包来运行处理操作，但无法对数据库进行任何更改。 无法在 SSMS 中查看模型数据库。|应用行筛选器。 仅能查询在行筛选器 DAX 公式中指定的数据。|  
|处理|成员可以通过运行包含处理命令的脚本或包来运行处理操作。 不能修改模型数据库架构。 无法查询数据。 无法查询在 SSMS 中的模型数据库。|不应用行筛选器。 此角色中没有可查询的数据|  
|管理员|成员可以对模型架构进行修改并可以查询模型设计器、 报表客户端和 SSMS 中的所有数据。|不应用行筛选器。 此角色中的所有数据均可查询。|  
  
##  <a name="bkmk_rowfliters"></a> Row filters  
 行筛选器定义表中可供特定角色的成员进行查询的行。 通过使用 DAX 公式为模型中的每个表定义行筛选器。  
  
 只能为具有“读取”和“读取和处理”权限的角色定义行筛选器。 默认情况下，如果没有为某一特定表定义行筛选器，则具有“读取”和“读取和处理”权限的角色的成员将能够查询表中的所有行，除非交叉筛选应用于其他表。  
  
 一旦为特定表定义了行筛选器后，求值结果必须为 TRUE/FALSE 值的 DAX 公式将定义可供该特定角色的成员进行查询的行。 未包含在 DAX 公式中的行将不可查询。 例如，对于具有以下行筛选器表达式的 Customers 表，Sales 角色的成员将只能看到 USA 中的客户：=Customers [Country] = “USA”。  
  
 行筛选器应用于指定的行以及相关行。 如果表具有多个关系，则筛选器将安全性应用于处于活动状态的关系。 行筛选器将与为相关表定义的其他行筛选器相交，例如：  
  
|表|DAX 表达式|  
|-----------|--------------------|  
|地区|=Region[Country]=”USA”|  
|ProductCategory|=ProductCategory[Name]=”Bicycles”|  
|中的|=Transactions[Year]=2008|  
  
 这些权限对于 Transactions 表的净效果是，将允许成员查询客户位于 USA、产品类别是自行车并且年份是 2008 的数据行。 用户将无法查询 USA 之外的任何事务、不是自行车的任何事务或者不在 2008 年发生的任何事务，除非用户是授予了这些权限的其他角色。  
  
 可使用筛选器 =FALSE() 来拒绝对整个表所有行的访问。  
  
### <a name="dynamic-security"></a>动态安全性  
 动态安全性提供了一种基于当前登录用户的用户名或从连接字符串返回的 CustomData 属性定义行级别安全性的方式。 为了实现动态安全性，您必须在模型中包含一个具有用户登录名（Windows 用户名）值的表以及一个可用于定义特定权限的字段；例如，一个具有登录 ID (domain\username) 的 dimEmployees 表以及一个针对每个员工的部门值。  
  
 为了实现动态安全性，您可以使用以下函数作为 DAX 公式的一部分来返回当前登录用户的用户名，或者返回连接字符串中的 CustomData 属性：  
  
|函数|Description|  
|--------------|-----------------|  
|[USERNAME 函数 (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f)|返回当前登录用户的 domain\username。|  
|[CUSTOMDATA 函数 (DAX)](http://msdn.microsoft.com/58235ad8-226c-43cc-8a69-5a52ac19dd4e)|返回连接字符串中的 CustomData 属性。|  
  
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
|@shouldalert|企业|  
|2|一般行政和管理|  
|3|库存管理|  
|4|生产|  
|5|质量保证|  
|6|研究和开发|  
|7|销售和营销|  
  
##  <a name="bkmk_testroles"></a> Testing roles  
 在创作模型项目时，可以使用“在 Excel 中分析”功能来测试已定义的角色的效用。 从模型设计器中的 **“模型”** 菜单中，当您单击 **“在 Excel 中分析”** 时，在打开 Excel 之前，将会出现 **“选择凭据和透视”** 对话框。 在此对话框中，您可以指定当前用户名、其他用户名、角色和一个用于连接作为数据源的工作区模型的透视。 若要了解详细信息，请参阅[在 Excel 中的分析](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)。  
  
##  <a name="bkmk_rt"></a> Related tasks  
  
|主题|Description|  
|-----------|-----------------|  
|[创建和管理角色](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md)|本主题中的任务说明如何使用 **“角色管理器”** 对话框来创建和管理角色。|  
  
## <a name="see-also"></a>请参阅  
 [透视](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [在 Excel 中分析](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)   
 [USERNAME 函数 (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f)   
 [LOOKUPVALUE 函数 (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab)   
 [CUSTOMDATA 函数 (DAX)](http://msdn.microsoft.com/58235ad8-226c-43cc-8a69-5a52ac19dd4e)  
  
  
