---
title: 设置模拟选项 (SSAS-多维) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c11064ecc87744999c31080e6a4d57a3849f5d2
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34026154"
---
# <a name="set-impersonation-options-ssas---multidimensional"></a>设置模拟选项（SSAS - 多维）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 Analysis Services 模型中创建 **data source** 对象时，您必须配置的一个设置是模拟选项。 此选项确定 Analysis Services 在执行与连接相关的本地操作（如加载 OLE DB 数据访问接口或在支持漫游配置文件的环境中解析用户配置文件信息）时是否采用特定 Windows 用户帐户的标识。  
  
 对于使用 Windows 身份验证的连接，模拟选项还确定对外部数据源执行查询的用户标识。 例如，如果你将模拟选项设置为 **contoso\dbuser**，则在处理期间用于检索数据的查询将以数据库服务器上的 **contoso\dbuser** 身份执行。  
  
 本主题说明在配置数据源对象时如何在 **“模拟信息”** 对话框中设置模拟选项。  
  
## <a name="set-impersonation-options-in-sql-server-data-tools"></a>在 SQL Server Data Tools 中设置模拟选项  
  
1.  在解决方案资源管理器中双击某一数据源以便打开数据源设计器。  
  
2.  在数据源设计器中单击 **“模拟信息”** 选项卡。  
  
3.  选择本主题的 [模拟选项](#bkmk_options) 中所述的一个选项。  
  
## <a name="set-impersonation-options-in-management-studio"></a>在 Management Studio 中设置模拟选项  
 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，通过针对这些对话框的以下属性单击省略号 (**...**) 按钮，打开“模拟信息”对话框：  
  
-   **“数据库属性”** 对话框（通过“数据源模拟信息”属性）。  
  
-   **“数据源属性”** 对话框（通过“模拟信息”属性）。  
  
-   **“程序集属性”** 对话框（通过“模拟信息”属性）。  
  
##  <a name="bkmk_options"></a> 模拟选项  
 对话框中的所有选项都可用，但并非所有选项都适合每种情况。 使用以下信息来确定最适合于您的情况的选项。  
  
 **使用特定用户名和密码**  
 选择此选项将使[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]对象使用此格式中指定的 Windows 用户帐户的安全凭据： *\<域名 >***\\***\<用户帐户名称 >*。  
  
 选择此选项可使用一个专用的最小权限的 Windows 用户标识，该用户标识是您为数据访问目的而专门创建的。 例如，如果您定期创建用于检索在报表中使用的数据的通用帐户，则可以在此处指定该帐户。  
  
 对于多维数据库，指定的凭据将用于执行处理、ROLAP 查询、外部绑定、本地多维数据集、挖掘模型、远程分区、链接对象以及从目标到源的同步。  
  
 对于 DMX OPENQUERY 语句，则忽略此选项，并且将使用当前用户的凭据而不是指定用户帐户的凭据。  
  
 **使用服务帐户**  
 选择此选项将使 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象使用与管理该对象的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务相关联的安全凭据。 这是默认选项。 在以前的版本中，这是唯一可以使用的选项。 若要在服务级别而不是单独的用户帐户级别监视数据访问，您可能会愿意选择此选项。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，根据您使用的不同操作系统，服务帐户可能是 NetworkService 或为特定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例创建的内置虚拟帐户。 如果您为使用 Windows 身份验证的连接选择服务帐户，请记住要为此帐户创建数据库登录名并授予读取权限，因为它将用于在处理期间检索数据。 有关服务帐户的详细信息，请参阅 [Configure Windows Service Accounts and Permissions](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)。  
  
> [!NOTE]  
>  使用数据库身份验证时，如果正在 Analysis Services 的专用虚拟帐户下运行服务，应选择 **“使用服务帐户”** 模拟选项。 此帐户将具有访问本地文件的权限。 如果服务以 NetworkService 身份运行，最好使用具有 **“允许在本地登录”** 权限的最小权限的 Windows 用户帐户。 根据您提供的帐户，您可能还需要授予对 Analysis Services 程序文件夹的文件访问权限。  
  
 对于多维数据库，服务帐户凭据将用于处理、ROLAP 查询、远程分区、链接对象以及从目标到源的同步。  
  
 对于 DMX OPENQUERY 语句、本地多维数据集和挖掘模型，即使您选择服务帐户选项，也将使用当前用户的凭据。 外部绑定不支持此服务帐户选项。  
  
> [!NOTE]  
>  如果服务帐户不具有对 Analysis Services 实例的管理员权限，在处理多维数据集的数据挖掘模型时会出错。 有关详细信息，请参阅 [挖掘结构：数据源是 OLAP 多维数据集时的处理问题](http://go.microsoft.com/fwlink/?LinkId=251610)。  
  
 **使用当前用户的凭据**  
 选择此选项将使 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 对象使用当前用户的安全凭据来处理外部绑定、DMX OPENQUERY、本地多维数据集和挖掘模型。  
  
 使用外部绑定的本地多维数据集和处理除外，多维数据库不支持此选项。  
  
 “默认值”或“继承”  
 此对话框对于在数据库级别设置的模拟选项使用“默认值”；而对于在数据源级别设置的模拟选项使用“继承”。  
  
 **“数据源 - 继承”选项**  
  
 在数据源级别， **“继承”** 指定 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 应使用父对象的模拟选项。 在多维模型中，父对象是 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。 通过选择 **“继承”** 选项，您可为此数据源以及属于同一个数据库的其他数据源集中管理模拟设置。 为使此选项有意义，请在数据库级别选择一个特定的 Windows 用户名和密码。 否则，结合对数据源使用 **“继承”** 以及对数据库使用 **“默认值”** 等效于使用服务帐户选项。  
  
 要在数据库级别指定 Windows 用户名和密码，请执行以下操作：  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中右键单击该数据库并选择“属性”。  
  
2.  在 **“数据源模拟信息”** 中，指定 Windows 用户名和密码。  
  
3.  右键单击每个数据源并查看其属性，以便确保每个数据源都在使用“继承”选项。  
  
 有关数据库级别的默认设置的详细信息，请参阅[设置多维数据库属性 (Analysis Services)](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md)。  
  
 **“数据库 – 默认值”选项**  

 对于多维数据库， **“默认值”** 意味着使用服务帐户，并将当前用户用于数据挖掘操作。  
  
## <a name="see-also"></a>另请参阅  
 [创建数据源（SSAS 多维）](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)   
 [设置数据源属性 & #40;SSAS 多维 & #41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md)   

  
  
