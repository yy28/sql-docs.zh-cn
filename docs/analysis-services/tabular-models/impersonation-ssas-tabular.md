---
title: Analysis Services 表格模型中的模拟 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 724d9220f156cb9b2a00e3bd12a15f35750de652
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52416010"
---
# <a name="impersonation"></a>Impersonation 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  本文提供了表格模型创建者的登录凭据时如何使用 Analysis services 连接到数据源导入和处理 （刷新） 数据的了解。  

##  <a name="bkmk_conf_imp_info"></a> 配置模拟  
 其中，和何种上下文中存在的模型确定如何配置模拟信息。 创建新模型项目时，模拟时，配置 SQL Server Data Tools (SSDT) 中连接到数据源导入数据。 一旦部署某一模型，可以通过使用 SQL Server Management Studio (SSMS) 模型数据库连接字符串属性中配置模拟。 对于 Azure Analysis Services 中的表格模型，可以使用 SSMS 或**形式查看：脚本**基于浏览器的设计器编辑 json 格式的 Model.bim 文件中的模式。
  
##  <a name="bkmk_how_imper"></a> 如何使用模拟  
  “模拟”是服务器应用程序（例如 Analysis Services）模拟某一客户端应用程序的身份的能力。 可以执行 analysis Services 使用服务帐户运行，但是，当服务器建立连接到数据源，它使用模拟，以便针对数据导入和处理访问检查。  
  
 用于模拟的凭据是不同于当前的登录的凭据。 登录的用户凭据用于特定的客户端的操作创建模型时。  
  
 务必要了解如何指定和受保护的这两个已登录的上下文之间的差异以及模拟凭据将使用用户凭据和使用其他模拟凭据的时间。  
  
 **理解服务器端凭据**  
 
导入或处理数据时的模拟凭据将用于连接到数据源并提取数据。 这是*服务器端*因为承载工作区数据库的 Analysis Services 服务器连接到数据源并提取数据的客户端应用程序的上下文中运行的操作。  
  
 在您将某个模型部署到 Analysis Services 服务器时，如果在部署该模型时工作区数据库处于内存中，则凭据将传递到该模型部署到的 Analysis Services 服务器。 在任何时候用户凭据都不要存储在磁盘上。  
  
 当已部署的模型处理数据源中的数据时，保留在内存中数据库的模拟凭据用于连接到数据源并提取数据。 由于此过程由管理模型数据库的 Analysis Services 服务器，这再次是服务器端操作。  
  
 **了解客户端凭据**  
  
 当创作新的模型或将数据源添加到现有模型，您连接到数据源，并选择要导入到模型表和视图。 表导入向导或获取 Data\Query 设计器预览和筛选功能，请参阅你导入的数据的示例。 您还可以指定筛选器以便排除不需要包括在模型中的数据。  
  
 同样，对于已创建的现有模型，则使用**表属性**对话框预览并筛选导入到表中的数据。  
  
 预览并筛选功能中，**表属性**，并**分区管理器**对话框是进程内*客户端*操作; 也就是说，在此期间执行的操作操作是不同于如何将数据源连接到和从数据源; 提取数据在服务器端操作。 用于预览和筛选数据的凭据是用户当前登录所用的凭据。 事实上，你的凭据。 
  
 在服务器端的过程中使用的凭据的分离和客户端操作可能会导致出现您所看到的内容以及导入或处理 （服务器端操作） 期间提取哪些数据不匹配。 如果凭据你当前使用登录和指定的模拟凭据不同，数据所示的预览并筛选功能或**表属性**对话框和导入期间提取的数据或进程可能会不同，具体取决于所需的数据源的凭据。  
  
> [!IMPORTANT]  
>  当创作的模型，请确保使用登录的凭据和为模拟指定的凭据具有足够的权限来从数据源提取数据。  
  
##  <a name="bkmk_imp_info_options"></a> 选项  
 配置模拟时，或者为现有数据源连接编辑属性时，指定以下选项之一：  
  
**表格 1400年和更高版本的模型**
 
|选项|Description|  
|------------|-----------------|  
|**模拟帐户**|指定模型使用的 Windows 用户帐户导入或处理来自数据源的数据。 域和用户帐户的名称使用以下格式：**\<域名 >\\< 用户帐户名\>**。|  
|**模拟当前用户**|指定应从数据源使用的发送请求的用户标识访问数据。 此模式仅适用于直接查询模式下。|  
|**模拟标识**|指定用户名即可访问数据源，但并不需要指定该帐户的密码。 Kerberos 委派，并指定应使用 S4U 身份验证，仅适用于此模式。|  
|**模拟服务帐户**|指定模型使用与管理该模型的 Analysis Services 服务实例关联的安全凭据。|  
|**模拟无人参与的帐户**|指定 Analysis Services 引擎应使用预配置的无人参与的帐户以访问数据。|  


**表格 1200年模型**
 
|选项|Description|  
|------------|-----------------|  
|**特定 Windows 用户名和密码**|此选项指定模型使用的 Windows 用户帐户导入或处理来自数据源的数据。 域和用户帐户的名称使用以下格式：**\<域名 >\\< 用户帐户名\>**。 在使用“表导入向导”创建新模型时，此为默认选项。|  
|**服务帐户**|此选项指定模型使用与管理该模型的 Analysis Services 服务实例相关联的安全凭据。|  
  
##  <a name="bkmk_impers_sec"></a> 安全性  
 用于模拟的凭据是保持在内存中由 VertiPaq™ 引擎。 凭据永远不会写入到磁盘。 如果工作区数据库不是内存中，部署模型时，将提示用户输入用于连接到数据源并提取数据的凭据。  
  
> [!NOTE]  
>  建议您为模拟凭据指定 Windows 用户帐户和密码。 Windows 用户帐户可以配置为使用连接到和从数据源中读取数据所需的最低权限。  
  

  
## <a name="see-also"></a>另请参阅  
 [DirectQuery 模式](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [数据源](../../analysis-services/tabular-models/data-sources-ssas-tabular.md)   
 [表格模型解决方案部署](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  
