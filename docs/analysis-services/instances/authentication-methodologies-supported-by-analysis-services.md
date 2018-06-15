---
title: Analysis Services 支持的身份验证方法 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fe2c4021792c3285165440fc0627aa7eab374882
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34019134"
---
# <a name="authentication-methodologies-supported-by-analysis-services"></a>Analysis Services 支持的身份验证方法
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  从客户端应用程序到 Analysis Services 实例的连接需要 Windows 身份验证（集成）。 您可以使用以下任意方法提供 Windows 用户标识：  
  
-   NTLM  
  
-   Kerberos（请参阅 [Kerberos 约束委派配置 Analysis Services](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)）  
  
-   连接字符串上的 EffectiveUserName  
  
-   基本或匿名（要求针对 HTTP 访问进行配置）  
  
-   已存储凭据  
  
 请注意，不支持声明身份验证。 不能使用 Windows 声明令牌访问 Analysis Services。 Analysis Services 客户端库仅使用 Windows 安全原则。 如果您的 BI 解决方案包括声明标识，您需要为每个用户提供 Windows 标识影子帐户，或者使用存储凭据访问 Analysis Services 数据。  
  
 有关 BI 和 Analysis Services 身份验证流的详细信息，请参阅 [Microsoft BI 身份验证和标识委托](http://go.microsoft.com/fwlink/?LinkID=286576)。  
  
##  <a name="bkmk_auth"></a> 了解您的身份验证选择  
 连接到 Analysis Services 数据库需要 Windows 用户或组标识和关联的权限。 该标识可能是需要查看报表的任何人使用的常规用途登录名，但是更可能包含单个用户的标识。  
  
 通常，表格或多维模型基于发出请求的用户将具有不同的数据访问级别（按对象或在数据本身内）。 为满足此要求，您可以使用 NTLM、Kerberos、EffectiveUserName 或基本身份验证。 所有这些技术都提供了使用每个连接传递不同用户标识的方法。 但是，这些选项的大部分受单跃点的限制。 只有具有委托的 Kerberos 允许原始用户标识跨多个计算机连接流到远程服务器上的后端数据存储区。  
  
 **NTLM**  
  
 对于指定 `SSPI=Negotiate`的连接，NTLM 是当 Kerberos 域控制器不可用时使用的备份身份验证子系统。 在 NTLM 下，只要请求是从客户端到服务器的直接连接，请求连接的用户具有对资源的权限且客户端和服务器计算机位于同一域中，则任何用户或客户端应用程序都可以访问服务器资源。  
  
 在多层解决方案中，NLTM 的单个跃点限制可能是主要约束。 可以在恰好一台远程服务器上模拟发出请求的用户标识，但不能进一步传播。 如果当前操作要求在多台计算机上运行的服务，您需要配置 Kerberos 约束委派，以重用后端服务器上的安全令牌。 或者，您可以使用存储的凭据或基本身份验证来传入通过单跃点连接的新标识信息。  
  
 **Kerberos 身份验证和 Kerberos 约束委派**  
  
 Kerberos 身份验证是 Active Directory 域中 Windows 集成安全性的基础。 与 NTLM 一样，Kerberos 下的模拟受单跃点的限制，除非您启用委托。  
  
 为了支持多跃点连接，Kerberos 提供约束委派和非约束委派，但是对于大多数方案，约束委派能更好保证安全性。 约束委派允许服务将用户标识的安全令牌传递给远程计算机上的指定下级服务。 对于多层应用程序，通常要求将来自中间层应用程序服务器的用户标识委托给某个后端数据库（如 Analysis Services）。 例如，基于用户标识返回不同数据的表格或多维模型可能要求来自中间层服务的标识委托，以避免用户重新输入凭据或以其他方式获取安全凭据。  
  
 约束委派需要在 Active Directory 中进行额外配置，其中请求的发送端和接收端上的服务均被显式授权用于委托。 尽管之前存在配置成本，但是配置服务后，将在 Active Directory 中独立管理密码更新。 您不必在应用程序中更新存储的帐户信息，如果使用存储的凭据选项（后文将详细说明），则需要这样做。  
  
 有关针对约束委派配置 Analysis Services 的详细信息，请参阅 [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)。  
  
> [!NOTE]  
>  Windows Server 2012 支持跨域的约束委派。 相反，在更低功能级别上的域（如 Windows Server 2008 或 2008 R2）中配置 Kerberos 约束委派要求客户端和服务器计算机是同一域的成员。  
  
 **EffectiveUserName**  
  
 EffectiveUserName 是用于将标识信息传递给 Analysis Services 的连接字符串属性。 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint 使用它在使用日志中记录用户活动。 Excel Services 和 PerformancePoint Services 可使用它检索 SharePoint 中的工作簿或仪表板使用的数据。 还可以在对 Analysis Services 实例执行操作的自定义应用程序或脚本中使用它。  
  
 有关在 SharePoint 中使用 EffectiveUserName 的详细信息，请参阅 [在 SharePoint Server 2010 中使用 Analysis Services EffectiveUserName](http://go.microsoft.com/fwlink/?LinkId=311905)。  
  
 **基本身份验证和匿名用户**  
  
 基本身份验证还提供作为特定用户连接到后端服务器的第四种方法。 使用基本身份验证，在连接字符串上传递 Windows 用户名和密码，引入其他网络加密要求以确保在传输中保护敏感信息。 使用基本身份验证的重要优势是身份验证请求可以跨域边界。  
  
 对于匿名身份验证，您可以将匿名用户标识设置为某一特定的 Windows 用户帐户（默认为 IUSR_GUEST）或者某一应用程序池标识。 该匿名用户帐户将用于 Analysis Services 连接，并且必须对 Analysis Services 实例具有数据访问权限。 使用此方法时，在连接上只使用与匿名帐户关联的用户标识。 如果您的应用程序要求额外标识管理，您需要选择其他方法或使用您提供的标识管理解决方案进行补充。  
  
 只有在针对 HTTP 访问配置 Analysis Services，使用 IIS 和 msmdpump.dll 建立连接后，基本身份验证和匿名用户才可用。 有关详细信息，请参阅 [在 Internet Information Services (IIS) 8.0 上配置对 Analysis Services 的 HTTP 访问](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)。  
  
 **Stored Credentials**  
  
 大多数中间层应用程序服务包括存储用户名和密码的功能以便以后从下级数据存储区检索数据，例如 Analysis Services 或 SQL Server 关系引擎。 这样，存储的凭据就提供了检索数据的第五种方法。 此方法的不足之处在于引入了与保持用户名和密码最新关联的维护开销以及在连接上使用单个标识。 如果您的解决方案需要原始调用方的标识，存储的凭据将无法满足要求。  
  
 有关存储的凭据的详细信息，请参阅[创建、修改和删除共享数据源 (SSRS)](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md) 和[将 Excel Services 与 SharePoint Server 2013 中的 Secure Store Service 一起使用](http://go.microsoft.com/fwlink/?LinkID=309869)。  
  
## <a name="see-also"></a>另请参阅  
 [将模拟用于传输安全](http://go.microsoft.com/fwlink/?LinkId=311727)   
 [在 Internet Information Services (IIS) 8.0 上配置对 Analysis Services 的 HTTP 访问](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)   
 [针对 Kerberos 约束委派对 Analysis Services 进行配置](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md)   
 [针对 Analysis Services 实例的 SPN 注册](../../analysis-services/instances/spn-registration-for-an-analysis-services-instance.md)   
 [连接到 Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
