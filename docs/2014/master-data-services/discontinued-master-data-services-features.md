---
title: SQL Server 2014 中的废止 Master Data Services 功能 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 3236cce0-cfd9-43f8-8be3-e8c8dff8f162
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 3f1eb85cb05c8284990d46241ed752515ef5504b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "65479444"
---
# <a name="discontinued-master-data-services-features-in-sql-server-2014"></a>SQL Server 2014 中不再支持的 Master Data Services 功能
  此主题介绍 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中不再可用的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]功能。  
  
## <a name="includesssql14includessssql14-mdmd-discontinued-features"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]停用的功能  
 此版本中没有废弃的功能。  
  
## <a name="includesssql11includessssql11-mdmd-discontinued-features"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]停用的功能  
  
### <a name="security"></a>安全性  
 为了简化安全权限的分配，您不能再向派生层次结构、显式层次结构和属性组等对象分配模型对象权限。  
  
-   派生层次结构权限现在基于模型。 例如，如果希望用户对派生层次结构具有权限，则必须将**更新**分配给模型对象。 然后，可以将 "**拒绝**" 权限分配给不希望用户访问的任何实体。  
  
-   显式层次结构权限现在基于实体。 例如，如果用户对某个帐户实体具有 "**更新**" 权限，则该实体的所有显式层次结构都将可更新。  
  
-   不能再在 "**用户和组权限**" 功能区域中分配属性组权限。 相反，在创建属性组的 "**系统管理**" 功能区域中，可以为用户和组授予对属性组的 "**更新**" 权限。 对属性组的**只读**权限不再可用。  
  
### <a name="staging-process"></a>临时过程  
 您不能使用新的临时过程来：  
  
-   创建或删除集合。  
  
-   在集合中添加或删除成员。  
  
-   重新激活成员和集合。  
  
 可以使用 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 临时过程来处理集合。  
  
### <a name="model-deployment-wizard"></a>模型部署向导  
 不能再使用[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序中的向导创建和部署包含数据的包。 可改为使用新的命令行实用程序。 有关详细信息，请参阅[部署模型 (Master Data Services)](deploying-models-master-data-services.md)。  
  
 仍可以使用该向导来创建和部署不包含数据的包。  
  
 此外，包只能部署到创建它们的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本中。 这意味着在 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 中创建的包不能部署到 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]。 您必须将包部署到 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 环境中，然后将数据库升级到 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]。  
  
### <a name="code-generation-business-rules"></a>代码生成业务规则  
 自动生成 Code 属性值的业务规则现在以不同的方式进行管理。 以前，若要为 Code 属性生成值，请在 "**业务规则**" 下的 "**系统管理**" 功能区域中将 "**默认属性" 设置为 "生成的值**" 操作。 现在，在 "**系统管理**" 中，您必须编辑该实体以启用自动生成的代码值。 有关详细信息，请参阅[自动创建代码 (Master Data Services)](automatic-code-creation-master-data-services.md)。  
  
 如果具有包含此类规则的 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 模型部署包，当您将数据库升级到 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 时，将排除该业务规则。  
  
### <a name="bulk-updates-and-exporting"></a>大容量更新和导出  
 在[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序中，不能再大容量更新多个成员的属性值。 若要进行批量更新，请使用临时过程或[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]。  
  
 在[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序中，不能再将成员导出到 Excel。 若要使用 Excel 中的成员，请[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]使用。  
  
### <a name="transactions"></a>事务  
 在 "**资源管理器**" 功能区域中，用户不能再恢复其自己的事务。 之前，用户可以还原他们对**资源管理器**中的数据所做的更改。 管理员仍可以为 "**版本管理**" 功能区域中的所有用户恢复事务。  
  
 批注现在是永久性的，且无法删除。 以前，批注被视为事务，可以通过还原事务来删除批注。  
  
### <a name="web-service"></a>Web 服务  
 
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 服务现在可应 Silverlight 的要求自动启用。 以前必须手动启用该 Web 服务。  
  
### <a name="powershell-cmdlets"></a>PowerShell Cmdlet  
 MDS 不再包括 PowerShell cmdlet。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 2014 中不推荐使用的 Master Data Services 功能](deprecated-master-data-services-features.md)  
  
  
