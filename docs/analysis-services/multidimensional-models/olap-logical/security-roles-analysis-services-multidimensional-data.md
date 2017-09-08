---
title: "安全角色 (Analysis Services-多维数据) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- storage [Analysis Services], roles
- Analysis Services objects, roles
- security [Analysis Services], roles
- roles [Analysis Services], about roles
- server roles [Analysis Services]
- database roles [Analysis Services]
- roles [Analysis Services]
- storing data [Analysis Services], roles
- access rights [Analysis Services], roles
ms.assetid: 5b7e9cef-ff68-4d8e-99bc-e0094ced1baa
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ee88f607ae1370746db12ea4b9f9f6acc98c4c09
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="security-roles--analysis-services---multidimensional-data"></a>安全角色（Analysis Services - 多维数据）
  中使用角色[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]可管理的安全性[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]对象和数据。 在基本术语中，角色相关联的 Microsoft Windows 用户和具有特定访问权限和权限定义对象的实例由管理组的安全标识符 (Sid) [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 中提供了两种类型的角色[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]:  
  
-   服务器角色，它是一个固定角色，用于提供对 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例的管理员访问权限。  
  
-   数据库角色，这些角色由管理员定义，用于控制非管理员用户对对象和数据的访问权限。  
  
 中的安全性[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]安全管理通过使用角色和权限。 角色为用户组。 用户（也称为成员）既可向角色中添加，也可从中删除。 对象的权限按照角色来指定，对于某一角色拥有权限的对象，该角色中的所有成员都可使用。 角色中的所有成员对这些对象具有相等的权限。 各对象都有其特定权限。 每个对象都对应一个所授权限的集合；对于同一对象，可授予不同的权限集。 对于对象权限集合中的单个权限，只能向其分配一个角色。  
  
## <a name="role-and-role-member-objects"></a>角色和角色成员对象  
 角色是用户（成员）集合的包含对象。 角色定义建立在用户的成员资格[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 由于权限是按角色分配的，所以用户必须先是某个角色的成员，然后才能访问对象。  
  
 <xref:Microsoft.AnalysisServices.Role> 对象由参数名称、ID 和成员组成。 成员是字符串的集合。 每个成员都包含有格式为“域\用户名”的用户名。 名称是包含角色名称的字符串。 ID 是包含角色的唯一标识符的字符串。  
  
### <a name="server-role"></a>服务器角色  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]服务器角色的实例中定义的 Windows 用户和组的管理访问权限[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 此角色的成员有权访问所有[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库和对象的实例上[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，并且可以执行以下任务：  
  
-   使用 SQL Server Management Studio 或 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 执行服务器级管理功能，包括创建数据库和设置服务器级属性。  
  
-   使用分析管理对象 (AMO) 通过编程方式执行管理功能。  
  
-   维护 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库角色。  
  
-   启动跟踪（并非用于处理事件，此操作可以由具有“处理”访问权限的数据库角色执行）。  
  
 每个 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例都具有一个服务器角色，用于定义哪些用户可以管理该实例。 该角色的名称和 ID 均为 Administrators，与数据库角色不同，服务器角色不能删除，也不能添加或删除权限。 换而言之，用户可以使用或不是管理员的实例[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，取决于该实例的服务器角色中是否包含他或她[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
### <a name="database-roles"></a>数据库角色  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库角色定义用户访问的对象和中的数据[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]数据库。 数据库角色作为 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 数据库中的单独对象进行创建，并且仅应用于在其中创建该角色的数据库。 Windows 用户和用户组由管理员包括在该角色中，管理员也可定义角色中的权限。  
  
 角色的权限允许成员访问和管理数据库以及数据库中的对象和数据。 每个权限都有一个或多个与其关联的访问权限，这些访问权限进而会使该权限更好地控制对数据库中特定对象的访问。  
  
## <a name="permission-objects"></a>Permission 对象  
 权限与特定角色的对象（多维数据集、维度等）相关联。 权限指定角色的成员可对该对象执行哪些操作。  
  
 <xref:Microsoft.AnalysisServices.Permission> 类是一个抽象类。 因此，您必须使用派生类定义相应对象的权限。 对于每个对象，均定义一个权限派生类。  
  
|对象|类|  
|------------|-----------|  
|<xref:Microsoft.AnalysisServices.Database>|<xref:Microsoft.AnalysisServices.DatabasePermission>|  
|<xref:Microsoft.AnalysisServices.DataSource>|<xref:Microsoft.AnalysisServices.DataSourcePermission>|  
|<xref:Microsoft.AnalysisServices.Dimension>|<xref:Microsoft.AnalysisServices.DimensionPermission>|  
|<xref:Microsoft.AnalysisServices.Cube>|<xref:Microsoft.AnalysisServices.CubePermission>|  
|<xref:Microsoft.AnalysisServices.MiningStructure>|<xref:Microsoft.AnalysisServices.MiningStructurePermission>|  
|<xref:Microsoft.AnalysisServices.MiningModel>|<xref:Microsoft.AnalysisServices.MiningModelPermission>|  
  
 下表列出了权限可能启用的操作：  
  
|操作|值|解释|  
|------------|------------|-----------------|  
|处理|{**true**, **false**}<br /><br /> Default=**false**|如果值为 **true**，则成员可以处理该对象以及该对象中包含的任何对象。<br /><br /> 处理权限不适用于挖掘模型。 <xref:Microsoft.AnalysisServices.MiningModel>始终从继承的权限<xref:Microsoft.AnalysisServices.MiningStructure>。|  
|读取定义|{**None**, **Basic**, **Allowed**}<br /><br /> Default=**None**|指定成员是否能读取与对象关联的数据定义 (ASSL)。<br /><br /> 如果值为 **Allowed**，则成员可读取与对象关联的 ASSL。<br /><br /> **Basic** 和 **Allowed** 由对象中包含的对象继承。 **Allowed** 可覆盖 **Basic** 和 **None**。<br /><br /> 对象的 DISCOVER_XML_METADATA 要求值为**Allowed** 。 创建链接对象和本地多维数据集时，要求值为**Basic** 。|  
|读取|{**None**, **Allowed**}<br /><br /> Default=**None** （DimensionPermission 除外，其中 default=**Allowed**）|指定成员是否可读取架构行集和数据内容。<br /><br /> 如果值为**Allowed** ，则可读取数据库，这样您就可发现数据库。<br /><br /> **允许**对多维数据集将给予用架构行集和访问权限的读取访问权限的多维数据集内容 (除非通过约束<xref:Microsoft.AnalysisServices.CellPermission>和<xref:Microsoft.AnalysisServices.CubeDimensionPermission>)。<br /><br /> **允许**维度授予读取权限的维度中的所有属性 (除非通过约束<xref:Microsoft.AnalysisServices.CubeDimensionPermission>)。 读取权限仅用于对 <xref:Microsoft.AnalysisServices.CubeDimensionPermission> 的静态继承。 对于维度，如果值为**None** ，则将隐藏维度，且仅授予对可聚合属性的默认成员的访问权限；如果维度包含不可聚合属性，则将会引发错误。<br /><br /> **允许**上<xref:Microsoft.AnalysisServices.MiningModelPermission>授予权限，请参阅中架构行集的对象，以便执行预测联接。<br /><br /> **NoteAllowed**需要读取或写入到数据库中的任何对象。|  
|写入|{**None**, **Allowed**}<br /><br /> Default=**None**|指定成员是否拥有对父对象的数据的写入权限。<br /><br /> 该权限适用于 <xref:Microsoft.AnalysisServices.Dimension>、<xref:Microsoft.AnalysisServices.Cube> 和 <xref:Microsoft.AnalysisServices.MiningModel> 子类。 它不适用于数据库<xref:Microsoft.AnalysisServices.MiningStructure>子类，用于生成验证错误。<br /><br /> **允许**上<xref:Microsoft.AnalysisServices.Dimension>授予写入权限的维度中的所有属性。<br /><br /> **允许**上<xref:Microsoft.AnalysisServices.Cube>授予写入单元格上定义为类型的分区的多维数据集的权限 = 写回。<br /><br /> **允许**上<xref:Microsoft.AnalysisServices.MiningModel>授予修改模型内容的权限。<br /><br /> **允许**上<xref:Microsoft.AnalysisServices.MiningStructure>没有任何特定的意义[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。<br /><br /> 注意： 写不能设置为**允许**除非读取也设置为**允许**|  
|Administer<br /><br /> 注意： 仅在数据库权限|{**true**, **false**}<br /><br /> Default=**false**|指定成员是否可管理数据库。<br /><br /> 如果值为**true** ，则将授予成员对数据库中所有对象的访问权限。<br /><br /> 成员可以拥有特定数据库的管理权限，但却不能拥有其他数据库的管理权限。|  
  
## <a name="see-also"></a>另请参阅  
 [权限和访问权限 &#40;Analysis Services-多维数据 &#41;](http://msdn.microsoft.com/library/59fa3573-f985-46cb-8042-7da71bd59a7b)   
 [授权访问对象和操作 &#40;Analysis Services &#41;](../../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
  
