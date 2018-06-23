---
title: 废弃的 SQL Server 2014 中的 Master Data Services 功能 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3236cce0-cfd9-43f8-8be3-e8c8dff8f162
caps.latest.revision: 12
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 46f5d4de97af6822ba110fe35e81df2d13a526ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124812"
---
# <a name="discontinued-master-data-services-features-in-sql-server-2014"></a>SQL Server 2014 中不再支持的 Master Data Services 功能
  此主题介绍 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 中不再可用的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]功能。  
  
## <a name="includesssql14includessssql14-mdmd-discontinued-features"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 废弃的功能  
 此版本中没有废弃的功能。  
  
## <a name="includesssql11includessssql11-mdmd-discontinued-features"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 废弃的功能  
  
### <a name="security"></a>Security  
 为了简化安全权限的分配，您不能再向派生层次结构、显式层次结构和属性组等对象分配模型对象权限。  
  
-   派生层次结构权限现在基于模型。 例如，如果你想让用户有权派生层次结构，则必须分配**更新**的模型对象。 然后可以将赋**拒绝**不希望用户具有访问权限的任何实体的访问权限。  
  
-   显式层次结构权限现在基于实体。 例如，如果用户具有**更新**到帐户实体的权限，然后所有显式层次结构的实体是否可以更新。  
  
-   属性组权限可以不再分配中**用户和组权限**功能区域。 相反，在**系统管理**创建属性组的位置的功能区域、 用户和组可以将提供**更新**属性组的权限。 **只读**属性组的权限已不再可用。  
  
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
 自动生成 Code 属性值的业务规则现在以不同的方式进行管理。 以前，若要生成为 Code 属性的值，你使用**为生成的值的默认属性**中的操作**系统管理**下的功能区域**业务规则**. 现在，在**系统管理**，必须编辑实体以启用自动生成的代码值。 有关详细信息，请参阅[自动创建代码 (Master Data Services)](automatic-code-creation-master-data-services.md)。  
  
 如果具有包含此类规则的 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 模型部署包，当您将数据库升级到 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 时，将排除该业务规则。  
  
### <a name="bulk-updates-and-exporting"></a>大容量更新和导出  
 在[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序中，不能再大容量更新多个成员的属性值。 若要执行批量更新，使用临时过程或[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]。  
  
 在[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序中，不能再将成员导出到 Excel。 若要使用在 Excel 中的成员，使用[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]。  
  
### <a name="transactions"></a>中的  
 在**资源管理器**功能区域中，用户将无法再还原它们自己的事务。 以前，用户无法还原他们中的数据所做的更改**资源管理器**。 管理员仍可以还原中的所有用户事务**版本管理**功能区域。  
  
 批注现在是永久性的，且无法删除。 以前，批注被视为事务，可以通过还原事务来删除批注。  
  
### <a name="web-service"></a>Web 服务  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web 服务现在可应 Silverlight 的要求自动启用。 以前必须手动启用该 Web 服务。  
  
### <a name="powershell-cmdlets"></a>PowerShell Cmdlet  
 MDS 不再包括 PowerShell cmdlet。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 中弃用的 Master Data Services 功能](deprecated-master-data-services-features.md)  
  
  