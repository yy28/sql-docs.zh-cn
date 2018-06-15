---
title: Analysis Services 表格模型中的模拟 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f32c63e8bc72b9d93ac30052d9c6bfa68bc4045a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34044591"
---
# <a name="impersonation"></a>模拟 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  本文提供了表格模型作者的登录凭据时如何使用的 Analysis services 连接到数据源导入和处理 （刷新） 数据的了解。  

##  <a name="bkmk_conf_imp_info"></a> 配置模拟  
 其中，和在什么上下文中存在的模型确定如何配置模拟信息。 创建新的模型项目时，模拟时连接到要导入数据的数据源配置 SQL Server Data Tools (SSDT) 中。 一旦部署某一模型，可以通过使用 SQL Server Management Studio (SSMS) 在模型数据库连接字符串属性中配置模拟。 对于 Azure Analysis Services 中的表格模型，你可以使用 SSMS 或**视为： 脚本**基于浏览器的设计器编辑 JSON 中的 Model.bim 文件中的模式。
  
##  <a name="bkmk_how_imper"></a> 如何使用模拟  
  “模拟”是服务器应用程序（例如 Analysis Services）模拟某一客户端应用程序的身份的能力。 可以执行 analysis Services 使用服务帐户运行，但是，当服务器建立了连接到数据源，它使用模拟以便访问检查数据导入和处理。  
  
 用于模拟凭据不同于你当前在使用登录的凭据。 登录的用户凭据将用于特定客户端操作，在创作模型时。  
  
 务必要了解如何指定和保护，以及在哪些这两个登录的上下文之间的差异上模拟凭据使用用户凭据，并且使用其他模拟凭据时。  
  
 **理解服务器端凭据**  
 
导入或处理数据时模拟凭据用于连接到数据源并提取数据。 这是*服务器端*因为承载工作区数据库的 Analysis Services 服务器连接到数据源并提取数据的客户端应用程序的上下文中运行的操作。  
  
 在您将某个模型部署到 Analysis Services 服务器时，如果在部署该模型时工作区数据库处于内存中，则凭据将传递到该模型部署到的 Analysis Services 服务器。 在任何时候用户凭据都不要存储在磁盘上。  
  
 当已部署的模型处理从数据源的数据时，保留在内存中数据库的模拟凭据用于连接到数据源并提取数据。 因为此过程由管理模型数据库的 Analysis Services 服务器处理，这是试服务器端操作。  
  
 **了解客户端凭据**  
  
 当创作一个新模型或将数据源添加到现有模型，您连接到数据源，并选择要导入到模型表和视图。 表导入向导或获取 Data\Query 设计器预览和筛选功能，请参阅你导入的数据的示例。 您还可以指定筛选器以便排除不需要包括在模型中的数据。  
  
 同样，对于已创建的现有模型，你使用**表属性**对话框预览并筛选导入到表的数据。  
  
 预览并筛选功能中，**表属性**，和**分区管理器**对话框处于进程内*客户端*操作; 即，已在此期间执行的操作操作与数据源连接到的方式不同，从数据源; 提取数据服务器端操作。 用于预览和筛选数据的凭据是用户当前登录所用的凭据。 事实上，你的凭据。 
  
 在服务器端期间使用的凭据分隔和客户端操作可能会导致中看到的内容以及哪些数据提取在导入或处理 （服务器端操作） 期间不匹配。 如果凭据您当前登录所使用模拟指定的凭据不同，数据会出现在预览并筛选功能或**表属性**对话框和导入过程中提取的数据或过程可能会不同，具体取决于所需的数据源的凭据。  
  
> [!IMPORTANT]  
>  在创作模型时，确保在使用登录的凭据和为模拟指定的凭据具有足够的权限从数据源提取数据。  
  
##  <a name="bkmk_imp_info_options"></a> 选项  
 配置模拟时，或者编辑现有数据源连接属性时，指定以下选项之一：  
  
**1400 和更高版本的表格模型**
 
|选项|Description|  
|------------|-----------------|  
|**模拟帐户**|指定模型使用 Windows 用户帐户导入或处理从数据源的数据。 域和用户帐户名称使用以下格式：**\<域名 >\\< 用户帐户名\>**。|  
|**模拟当前用户**|指定应从数据源使用的发送请求的用户的标识访问数据。 此模式下仅适用于直接查询模式。|  
|**模拟标识**|指定一个用户名，以访问数据源，但并不需要指定该帐户的密码。 Kerberos 委派已启用并指定应使用 S4U 身份验证，仅适用于此模式。|  
|**模拟服务帐户**|指定模型使用与管理该模型的 Analysis Services 服务实例关联的安全凭据。|  
|**模拟无人参与的帐户**|指定 Analysis Services 引擎应使用预配置的无人参与的帐户来访问数据。|  


**表格 1200年模型**
 
|选项|Description|  
|------------|-----------------|  
|**特定 Windows 用户名和密码**|此选项指定模型使用 Windows 用户帐户导入或处理从数据源的数据。 域和用户帐户名称使用以下格式：**\<域名 >\\< 用户帐户名\>**。 在使用“表导入向导”创建新模型时，此为默认选项。|  
|**服务帐户**|此选项指定模型使用与管理该模型的 Analysis Services 服务实例相关联的安全凭据。|  
  
##  <a name="bkmk_impers_sec"></a> 安全性  
 与模拟一起使用的凭据是持久的内存中由 VertiPaq™ 引擎。 凭据永远不会写入到磁盘。 如果部署模型时，工作区数据库不是内存中，被提示用户输入用于连接到数据源并提取数据的凭据。  
  
> [!NOTE]  
>  建议您为模拟凭据指定 Windows 用户帐户和密码。 Windows 用户帐户可以配置为使用连接到和从数据源读取数据所需的最低权限。  
  

  
## <a name="see-also"></a>另请参阅  
 [DirectQuery 模式](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [数据源](../../analysis-services/tabular-models/data-sources-ssas-tabular.md)   
 [表格模型解决方案部署](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
