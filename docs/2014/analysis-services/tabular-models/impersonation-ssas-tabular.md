---
title: 模拟 (SSAS 表格) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: fcc79e96-182a-45e9-8ae2-aeb440e9bedd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6455a83328f973004f6c0e7ff39f574413693d94
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48111954"
---
# <a name="impersonation-ssas-tabular"></a>模拟（SSAS 表格）
  本主题帮助表格模型作者了解在连接到数据源以便导入和处理（刷新）数据时 Analysis Services 如何使用登录凭据。  
  
 本文包含以下各节：  
  
-   [优势](#bkmk_how_imper)  
  
-   [选项](#bkmk_imp_info_options)  
  
-   [Security](#bkmk_impers_sec)  
  
-   [导入模型时的模拟](#bkmk_imp_newmodel)  
  
-   [配置模拟](#bkmk_conf_imp_info)  
  
##  <a name="bkmk_how_imper"></a> 优势  
  “模拟”是服务器应用程序（例如 Analysis Services）模拟某一客户端应用程序的身份的能力。 但在服务器建立与数据源的连接时，Analysis Services 使用服务帐户运行，它使用模拟以便可以执行针对数据导入和处理的访问检查。  
  
 用于模拟的凭据不同于当前登录的用户所采用的凭据。 在创作模型时，将登录的用户凭据用于特定的客户端操作。  
  
 理解指定和保护模拟凭据的方式以及当前登录用户的凭据和其他凭据所用于的上下文之间的差异是十分重要的。  
  
 **理解服务器端凭据**  
  
 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，通过使用“表导入向导”中的 **“模拟信息”** 页，或者通过在 **“现有连接”** 对话框中编辑现有的数据源连接，为每个数据源指定凭据。  
  
 在导入或处理数据时，使用在 **“模拟信息”** 页中指定的凭据连接到数据源并提取数据。 这是在客户端应用程序的上下文中运行的“服务器端”  操作，因为承载工作区数据库的 Analysis Services 服务器连接到数据源并提取数据。  
  
 在您将某个模型部署到 Analysis Services 服务器时，如果在部署该模型时工作区数据库处于内存中，则凭据将传递到该模型部署到的 Analysis Services 服务器。 在任何时候用户凭据都不要存储在磁盘上。  
  
 在某个已部署的模型处理来自某个数据源的数据时，在内存中数据库中保持的模拟凭据将用于连接到该数据源并提取数据。 因为此过程是由管理模型数据库的 Analysis Services 服务器处理的，所以这个操作也是服务器端操作。  
  
 **理解客户端凭据**  
  
 当您创作一个新模型或者向现有模型添加数据源时，使用“表导入向导”连接到数据源并且选择要导入到模型中的表和视图。 在“表导入向导”的“选择表和视图”页中，可使用“预览并筛选”功能查看将导入的数据的示例（限制为 50 行）。 您还可以指定筛选器以便排除不需要包括在模型中的数据。  
  
 同样，对于已创建的现有模型，您可以使用 **“编辑表属性”** 对话框预览并筛选导入到表中的数据。 此处的预览和筛选功能在功用上与“表导入向导”的 **“选择表和视图”** 页上的 **“预览并筛选”** 功能相同。  
  
 “预览并筛选”功能与“表属性”和“分区管理器”对话框均为进程中客户端操作；也就是说，在此操作过程中所做的工作不同于连接到数据源和从数据源提取数据的方式；后两种操作都是服务器端操作。 用于预览和筛选数据的凭据是用户当前登录所用的凭据。 客户端操作始终使用当前用户的 Windows 凭据来连接到数据源。  
  
 由于在服务器端和客户端操作期间对凭据的使用是分隔开来的，因此，可能导致用户使用“预览并筛选”功能或“表属性”对话框所看到的内容（客户端操作）与导入或处理期间提取的数据（服务器端操作）出现不匹配。 如果当前登录的用户所用的凭据和指定的模拟凭据不同，则根据数据源所要求的凭据，在 **“预览并筛选”** 功能或 **“表属性”** 对话框中看到的数据与在导入或处理期间提取的数据可能会不同。  
  
> [!IMPORTANT]  
>  在创作模型时，请确保当前登录的用户所用的凭据和为模拟指定的凭据具有足够的权限来从数据源提取数据。  
  
##  <a name="bkmk_imp_info_options"></a> 选项  
 配置模拟时，或者在 Analysis Services 中为现有数据源连接编辑属性时，您可以指定以下选项之一：  
  
|选项|ImpersonationMode<sup>1</sup>|Description|  
|------------|-----------------------------------|-----------------|  
|**特定 Windows 用户名和密码** <sup>2</sup>|ImpersonateWindowsUserAccount|此选项指定模型使用 Windows 用户帐户从数据源导入或处理数据。 域和用户帐户的名称使用以下格式：**\<域名 >\\< 用户帐户名\>**。 在使用“表导入向导”创建新模型时，此为默认选项。|  
|**服务帐户**|ImpersonateServiceAccount|此选项指定模型使用与管理该模型的 Analysis Services 服务实例相关联的安全凭据。|  
  
 <sup>1</sup>ImpersonationMode 指定的值[DataSourceImpersonationInfo 元素&#40;ASSL&#41; ](../scripting/properties/impersonationinfo-element-assl.md)上的数据源的属性。  
  
 <sup>2</sup>时使用此选项时，如果从内存中，由于重新启动中删除工作区数据库或**工作区保持期**属性设置为**从内存中的卸载**或**从工作区中删除**，并且由该模型项目已关闭，在后续会话中，如果你尝试处理表数据，系统会提示输入每个数据源的凭据。 同样，如果从内存中删除某个已部署的模型数据库，则系统将会提示您输入为每个数据源输入凭据。  
  
##  <a name="bkmk_impers_sec"></a> Security  
 用于模拟的凭据由与 Analysis Services 服务器相关联的 xVelocity 内存中分析引擎 (VertiPaq)™ 保持在内存中（该服务器管理工作区数据库或已部署的模型）。  任何时候都不要将凭据写入磁盘中。 如果在部署模型时工作区数据库不在内存中，则系统将提示用户输入用于连接到数据源和提取数据的凭据。  
  
> [!NOTE]  
>  建议您为模拟凭据指定 Windows 用户帐户和密码。 可以将 Windows 用户帐户配置为连接到数据源和从数据源读取数据所需的最低权限。  
  
##  <a name="bkmk_imp_newmodel"></a> 导入模型时的模拟  
 与可以使用若干不同的模拟模式支持进程外数据收集的表格模型不同，PowerPivot 仅使用一个模式，即 ImpersonateCurrentUser。 因为 PowerPivot 始终在进程中运行，所以，它使用当前登录的用户的凭据连接到数据源。 对于表格模型，当前登录的用户的凭据仅用于“表导入向导”中的 **“预览并筛选”** 功能以及在查看 **“表属性”** 时。 在将数据导入或处理到工作区数据库中或者在将数据导入或处理到已部署的模型中时，使用模拟凭据。  
  
 在通过导入现有 PowerPivot 工作簿来创建新模型时，默认情况下，模型设计器将对模拟进行配置以便使用服务帐户 (ImpersonateServiceAccount)。 建议您将从 PowerPivot 导入的模型上的模拟凭据更改为 Windows 用户帐户。 已导入 PowerPivot 工作簿并在模型设计器中创建新模型后，你可以通过更改凭据**现有连接**对话框。  
  
 在通过从 Analysis Services 服务器上的现有模型导入来创建新模型时，模拟凭据将从现有模型数据库传递到新的模型工作区数据库。 如有必要，您可以使用 **“现有连接”** 对话框更改新模型上的凭据。  
  
##  <a name="bkmk_conf_imp_info"></a> 配置模拟  
 模型所处的环境将确定配置模拟信息的方式。 对于在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中创作的模型，您可以在“表导入向导”的 **“模拟信息”** 页中配置模拟信息，也可以通过在 **“现有连接”** 对话框上编辑数据源连接来配置模拟信息。 若要查看现有连接，请在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]的 **“模型”** 菜单中单击 **“现有连接”**。  
  
 对于部署到 Analysis Services 服务器的模型，可以通过单击省略号 （...） 的配置模拟信息**数据源模拟信息**属性中的**数据库属性**对话框中的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 [DirectQuery 模式（SSAS 表格）](directquery-mode-ssas-tabular.md)   
 [数据源&#40;SSAS 表格&#41;](../data-sources-ssas-tabular.md)   
 [表格模型解决方案部署&#40;SSAS 表格&#41;](tabular-model-solution-deployment-ssas-tabular.md)  
  
  
