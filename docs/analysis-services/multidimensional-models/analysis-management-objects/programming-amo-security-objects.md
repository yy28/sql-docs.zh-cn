---
title: "编程 AMO 安全对象 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- programming [AMO]
- Analysis Management Objects, security
- AMO, security
ms.assetid: 5d963721-6e6e-46eb-bc9b-18724dd0b751
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0b81d5b81df182309384c5d647a4251688bb1489
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="programming-amo-security-objects"></a>AMO 安全对象编程
  在[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，编程安全对象或运行使用 AMO 安全对象的应用程序需要是服务器管理员组或数据库管理员组的成员。 服务器管理员和数据库管理员将访问级别由[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中，对所有对象的用户访问权限是通过分配给该对象的角色和权限的组合获得的。 有关详细信息，请参阅[AMO 安全类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-security-classes.md)。  
  
## <a name="role-and-permission-objects"></a>Role 和 Permission 对象  
 服务器角色在集合中包含且只能包含一个角色，即 Administrators 角色。 不能向服务器角色集合添加新角色。 Administrators 角色中的成员身份允许对服务器中的每个对象的完全访问。  
  
 <xref:Microsoft.AnalysisServices.Role> 对象在数据库级别创建。 角色维护仅需要向角色添加成员或从角色中删除成员，以及对 <xref:Microsoft.AnalysisServices.Database> 对象添加或删除角色。 如果存在任何与该角色关联的 <xref:Microsoft.AnalysisServices.Permission> 对象，则不能删除该角色。 若要删除角色，必须在 <xref:Microsoft.AnalysisServices.Permission> 对象中搜索所有 <xref:Microsoft.AnalysisServices.Database> 对象，再从权限中删除 <xref:Microsoft.AnalysisServices.Role>，然后才能从 <xref:Microsoft.AnalysisServices.Role> 中删除 <xref:Microsoft.AnalysisServices.Database>。  
  
 权限定义对在其中提供权限的对象所启用的操作。 权限可提供给以下对象：<xref:Microsoft.AnalysisServices.Database>、<xref:Microsoft.AnalysisServices.DataSource>、<xref:Microsoft.AnalysisServices.Dimension>、<xref:Microsoft.AnalysisServices.Cube>、<xref:Microsoft.AnalysisServices.MiningStructure> 和 <xref:Microsoft.AnalysisServices.MiningModel>。 权限维护包括通过对应的访问属性来授予或撤消所启用的访问权限。 对于每个启用的访问权限，都有一个可被设置为所需访问级别的属性。 可以为以下操作定义访问权限：Process、ReadDefinition、Read、Write 和 Administer。 只能对 <xref:Microsoft.AnalysisServices.Database> 对象定义 Administer 访问权限。 数据库管理员安全级别在为该角色授予 Administer 数据库权限时获得。  
  
 下面的示例创建四个角色：Database Administrators、Processors、Writers 和 Readers。  
  
 Database Administrators 可以管理提供的数据库。  
  
 Processors 可以处理数据库中的所有对象并验证结果。 若要验证结果，必须为提供的多维数据集显式启用对数据库对象的读取访问权限，因为读取权限不能应用于子对象。  
  
 Writers 可以读取和写入提供的多维数据集，单元访问权限限制为客户维度中的“United States”。  
  
 Readers 可以读取提供的多维数据集，单元访问权限限制为客户维度中的“United States”。  
  
```  
static public void CreateRolesAndPermissions(Database db, Cube cube)  
{  
    Role role;  
    DatabasePermission dbperm;  
    CubePermission cubeperm;  
  
    #region Create the Database Administrators role  
  
    // Create the Database Administrators role.  
    role = db.Roles.Add("Database Administrators");  
    role.Members.Add(new RoleMember("")); // e.g. domain\user  
    role.Update();  
  
    // Assign administrative permissions to this role.  
    // Members of this role can perform any operation within the database.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Administer = true;  
    dbperm.Update();  
  
    #endregion  
  
    #region Create the Processors role  
  
    // Create the Processors role.  
    role = db.Roles.Add("Processors");  
    role.Members.Add(new RoleMember("")); // e.g. myDomain\johndoe  
    role.Update();  
  
    // Assign Read and Process permissions to this role.  
    // Members of this role can process objects in the database and query them to verify results.  
    // Process permission applies to all contained objects, i.e. all dimensions and cubes.  
    // Read permission does not apply to contained objects, so we must assign the permission explicitly on the cubes.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Process = true;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    cubeperm.Update();  
  
    #endregion  
  
    #region Create the Writers role  
  
    // Create the Writers role.  
    role = db.Roles.Add("Writers");  
    role.Members.Add(new RoleMember("")); // e.g. redmond\johndoe  
    role.Update();  
  
    // Assign Read and Write permissions to this role.  
    // Members of this role can discover, query and writeback to the Adventure Works cube.  
    // However cell access and writeback is restricted to the United States (in the Customer dimension).  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    cubeperm.Write = WriteAccess.Allowed;  
    cubeperm.CellPermissions.Add(new CellPermission(CellPermissionAccess.Read, "[Customer].[Country-Region].CurrentMember is [Customer].[Country-Region].[Country-Region].&[United States]"));  
    cubeperm.CellPermissions.Add(new CellPermission(CellPermissionAccess.ReadWrite, "[Customer].[Country-Region].CurrentMember is [Customer].[Country-Region].[Country-Region].&[United States]"));  
    cubeperm.Update();  
  
    #endregion  
  
    #region Create the Readers role  
  
    // Create the Readers role.  
    role = db.Roles.Add("Readers");  
    role.Members.Add(new RoleMember("")); // e.g. redmond\johndoe  
    role.Update();  
  
    // Assign Read permissions to this role.  
    // Members of this role can discover and query the Adventure Works cube.  
    // However the Customer dimension is restricted to the United States.  
    dbperm = db.DatabasePermissions.Add(role.ID);  
    dbperm.Read = ReadAccess.Allowed;  
    dbperm.Update();  
  
    cubeperm = cube.CubePermissions.Add(role.ID);  
    cubeperm.Read = ReadAccess.Allowed;  
    Dimension dim = db.Dimensions.GetByName("Customer");  
    DimensionAttribute attr = dim.Attributes.GetByName("Country-Region");  
    CubeDimensionPermission cubedimperm = cubeperm.DimensionPermissions.Add(dim.ID);  
    cubedimperm.Read = ReadAccess.Allowed;  
    AttributePermission attrperm = cubedimperm.AttributePermissions.Add(attr.ID);  
    attrperm.AllowedSet = "{[Customer].[Country-Region].[Country-Region].&[United States]}";  
    cubeperm.Update();  
  
    #endregion  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.AnalysisServices>   
 [引入 AMO 类](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [编程 AMO 安全对象](../../../analysis-services/multidimensional-models/analysis-management-objects/programming-amo-security-objects.md)   
 [权限和访问权限 &#40;Analysis Services-多维数据 &#41;](http://msdn.microsoft.com/library/59fa3573-f985-46cb-8042-7da71bd59a7b)   
 [逻辑体系结构 &#40;Analysis Services-多维数据 &#41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [数据库对象 &#40;Analysis Services-多维数据 &#41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
