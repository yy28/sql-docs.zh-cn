---
title: 使用报表管理器创建模型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report models [Reporting Services], creating
- Report Manager [Reporting Services], model creation
ms.assetid: 8e5d2bd3-48ec-45f3-afee-6d86797c8f28
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7b67e2a7048520d8a411789e501dbbe545d3cc02
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109664"
---
# <a name="create-a-model-using-report-manager"></a>使用报表管理器创建模型
  您可以使用报表管理器从 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多维数据集、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库或 Oracle 数据库生成模型。 报表模型是从已发布到报表服务器上的共享数据源中生成。 如果尚未拥有共享数据源，则必须先创建一个。  
  
 生成的报表模型完全基于共享数据源的架构。 您无法选择将数据源的哪些部分包含在模型中，也无法编辑所生成模型的规则或元数据。 不过，您可以在模型生成之后设置其属性，并定义用来限制访问整个或部分模型的角色分配。  
  
> [!NOTE]  
>  使用报表管理器或[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2007 [!INCLUDE[SPS2010](../includes/sps2010-md.md)]生成的基于 Oracle 的模型将包含数据库对象，这些对象是用于连接到 Oracle 数据源的用户帐户架构的一部分。 该用户帐户名在数据源属性凭据中指定。  
  
### <a name="to-create-a-new-data-source-for-a-report-model-using-report-manager"></a>使用报表管理器为报表模型创建新数据源  
  
1.  在 Web 浏览器的地址栏中，键入报表服务器的 URL。  
  
2.  单击 **“新建数据源”**。  
  
3.  在 **“名称”** 框中，为数据源输入名称。  
  
4.  根据需要，可以在 **“说明”** 文本框中输入模式的简短说明。  
  
5.  确认选中了 **“启用此数据源”** 复选框。  
  
6.  在 **“连接类型”** 列表中，选择要连接的数据源类型。 连接类型必须是以下类型之一： **Oracle**、 **Microsoft SQL Server** 或 **Microsoft SQL Server Analysis Services**。  
  
7.  在 **“连接字符串”** 框中，输入指向数据库的连接字符串。  
  
8.  选择报表生成器用户连接数据库需要使用的连接方法。  
  
    -   Windows 身份验证：如果希望操作系统对 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用户进行身份验证，请选择此选项。 如果选择此选项，则允许 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 使用 Windows 安全功能（如密码加密）对用户进行身份验证。 极力建议选择此选项。  
  
    -   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]身份验证：如果希望用户使用您创建的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]登录帐户，请选择此选项。 用户必须提供有效的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 登录名和密码。  
  
        > [!CAUTION]  
        >  请尽可能使用 Windows 身份验证。  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-create-a-report-model-using-report-manager"></a>使用报表管理器创建报表模型  
  
1.  在报表管理器中，选择要用于模型的数据源。  
  
     此时，将显示“属性”页。  
  
2.  确保为数据源指定的选项满足需要。  
  
3.  单击 **“生成模型”**。  
  
     此时，将显示数据源的“常规”页。  
  
4.  在 **“名称”** 框中，为报表模型输入名称。  
  
5.  在 **“说明”** 框中，输入对模型的简要说明。  
  
6.  若要指定新的位置保存报表模型，请单击 **“更改位置”**。  
  
     默认情况下，报表模型将保存到报表管理器主文件夹中。  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     此时，将创建报表模型并会将其保存到您指定的位置。 您可以使用报表管理器分配对此模型的权限。  
  
## <a name="see-also"></a>另请参阅  
 [授予对本机模式报表服务器的权限](security/granting-permissions-on-a-native-mode-report-server.md)   
 [Reporting Services 中的数据连接、数据源和连接字符串](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [“新建数据源”页（报表管理器）](../../2014/reporting-services/new-data-source-page-report-manager.md)  
  
  
