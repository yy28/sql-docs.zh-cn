---
title: AMO 安全对象的编程 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- programming [AMO]
- Analysis Management Objects, security
- AMO, security
ms.assetid: 5d963721-6e6e-46eb-bc9b-18724dd0b751
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7cd595825659b303e9bb705ce4fd9051a76f9f61
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48120777"
---
# <a name="programming-amo-security-objects"></a>AMO 安全对象编程
  在中[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，安全对象的编程或运行使用 AMO 安全对象的应用程序需要服务器管理员组或数据库管理员组的成员。 服务器管理员和数据库管理员是所需的访问级别由提供[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
 在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中，对所有对象的用户访问权限是通过分配给该对象的角色和权限的组合获得的。 有关详细信息，请参阅[AMO 安全类](amo-security-classes.md)。  
  
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
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.AnalysisServices>   
 [AMO 类简介](amo-classes-introduction.md)   
 [AMO 安全对象的编程](programming-amo-security-objects.md)   
 [权限和访问权限&#40;Analysis Services-多维数据&#41;](https://msdn.microsoft.com/library/ms174786(v=sql.120).aspx)   
 [保护 Analysis Services 实例](https://technet.microsoft.com/library/ms175663\(v=sql.110\).aspx)   
 [逻辑体系结构&#40;Analysis Services-多维数据&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [数据库对象&#40;Analysis Services-多维数据&#41;](../olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
