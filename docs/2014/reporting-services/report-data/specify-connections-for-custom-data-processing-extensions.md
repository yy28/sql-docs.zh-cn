---
title: 指定用于自定义数据处理扩展插件的连接 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- custom data processing extensions [Reporting Services]
- IDbConnection interface, connection strings
- impersonation [Reporting Services]
- IDbConnectionExtension interface, connection strings
- data sources [Reporting Services], security
- connection strings [Reporting Services]
- credentials [Reporting Services]
- authentication [Reporting Services]
- external data sources [Reporting Services]
- data processing extensions [Reporting Services], connections
ms.assetid: 2cddc9ea-0e28-4350-80ae-332412908e47
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: ffebeccb4b024434edf54990229ea9f001f39704
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56027648"
---
# <a name="specify-connections-for-custom-data-processing-extensions"></a>指定用于自定义数据处理扩展插件的连接
  您可以在报表服务器上创建或使用第三方自定义数据处理扩展插件来增强支持的数据源的数据处理能力，或者支持默认 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 安装中不可用的其他类型的数据源。 对连接的处理会因实现方式的不同而有所不同。 数据处理扩展插件可能具有下列实现方式：  
  
-   自定义 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 数据提供程序（如果要访问 DB2.NET、Oracle、ODP.NET 或 Teradata 数据源中的数据，则可以使用自定义 .NET 数据提供程序）  
  
-   支持 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>  
  
-   支持 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>  
  
> [!NOTE]  
>  请联系第三方提供商以了解如何实现自定义数据处理扩展插件。  
  
## <a name="impersonation-and-custom-data-processing-extensions"></a>模拟和自定义数据处理扩展插件  
 如果你的自定义数据处理扩展插件使用模拟功能连接到数据源，则必须在 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> 或 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension> 接口上使用 Open 方法来发出请求。 或者，可以存储用户标识对象 (System.Security.Principal.WindowsIdentity)，然后在其他数据处理扩展插件 API 中重用该对象。  
  
 在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的早期版本中，所有自定义数据处理扩展插件都通过用户模拟进行调用。 在此版本中，只有 Open 方法将在模拟用户时进行调用。 如果你的现有数据处理扩展插件要求具有集成安全性，则必须修改代码以使用 Open 方法或存储用户标识对象。  
  
## <a name="connections-for-custom-net-framework-data-providers"></a>用于自定义 .NET Framework 数据访问接口的连接  
 将报表配置为使用特定的数据源时，您可以设置确定数据源类型、连接字符串以及用于访问数据源的凭据的属性。 下表介绍 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 数据访问接口支持的凭据类型。 有关设置报表数据源属性的详细信息，请参阅 [为报表数据源指定凭据和连接信息](specify-credential-and-connection-information-for-report-data-sources.md)。  
  
|凭据|连接|  
|-----------------|-----------------|  
|集成安全性|如果您的数据访问接口支持 Windows 集成安全性，则可以使用该安全性。 这种情况下将使用当前用户的凭据来发送请求。<br /><br /> 定义连接字符串时，请确保包括指定集成安全性的参数（例如，对于到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源的连接，其连接字符串中可能包括 `Integrated Security=SSPI`）。|  
|Windows 身份验证|如果您的数据访问接口支持 Windows 域用户帐户，则可以使用该帐户。 在调用数据处理扩展插件之前，报表服务器将模拟该用户帐户。<br /><br /> 定义连接字符串时，请确保包括指定集成安全性的参数（例如，对于到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源的连接，其连接字符串中可能包括 `Integrated Security=SSPI`）。|  
|数据库凭据|通过自定义 .NET 数据访问接口建立的连接不支持数据库身份验证。 在任何情况下，报表服务器都将无法进行连接。|  
|无凭据|您可以将无凭据选项用于自定义 .NET 数据访问接口。 如果指定了无人参与的执行帐户，则连接字符串将确定使用的凭据。 报表服务器将模拟无人参与的执行帐户来建立连接。<br /><br /> 如果未定义无人参与的执行帐户，则报表服务器将无法进行连接。 有关定义此帐户的详细信息，请参阅 [配置无人参与的执行帐户（SSRS 配置管理器）](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)。|  
  
## <a name="connections-for-idbconnection"></a>IDbConnection 连接  
 如果要使用仅支持 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection>的自定义数据处理扩展插件，则必须按以下方式指定连接：  
  
1.  配置无人参与的执行帐户。 使用 `IDbConnection` 建立连接时，需要配置此帐户。 建立连接时，报表服务器将模拟此帐户。  
  
2.  将报表上的数据源属性配置为使用 **“无凭据”**。  
  
3.  将用于连接到数据源的凭据放置在连接字符串中。  
  
 使用 `IDbConnection` 时，不支持下列凭据类型：集成安全性、Windows 用户帐户以及数据库凭据。 如果数据源连接使用这些选项，则无法在报表服务器中进行连接。  
  
## <a name="connections-for-idbconnectionextension"></a>IDbConnectionExtension 连接  
 如果要使用支持 <xref:Microsoft.ReportingServices.DataProcessing.IDbConnectionExtension>的自定义数据处理扩展插件，则必须按以下方式指定连接：  
  
|凭据|连接|  
|-----------------|-----------------|  
|集成安全性|如果您的数据访问接口支持 Windows 集成安全性，则可以将该安全性用于使用 `IDbConnectionExtension` 的自定义数据处理扩展插件。<br /><br /> 定义连接字符串时，请确保包括指定集成安全性的参数（例如，对于到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源的连接，其连接字符串中可能包括 `Integrated Security=SSPI`）。|  
|Windows 身份验证|如果您的数据访问接口支持 Windows 域用户帐户，则可以将该帐户用于使用 `IDbConnectionExtension` 的自定义数据处理扩展插件。<br /><br /> 在调用数据处理扩展插件之前，报表服务器将模拟该用户帐户。 定义连接字符串时，请确保包括指定集成安全性的参数（例如，对于到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源的连接，其连接字符串中可能包括 `Integrated Security=SSPI`）。|  
|数据库凭据|您可以使用数据库身份验证针对使用 `IDbConnectionExtension` 的自定义数据处理扩展插件配置连接。|  
|无凭据|如果指定了无人参与的执行帐户，则连接字符串将确定使用的凭据。<br /><br /> 如果未定义无人参与的执行帐户，则报表服务器将无法进行连接。|  
  
## <a name="see-also"></a>请参阅  
 [配置无人参与的执行帐户（SSRS 配置管理器）](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
 [为报表数据源指定凭据和连接信息](specify-credential-and-connection-information-for-report-data-sources.md)   
 [数据连接、 数据源和 Reporting Services 中的连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [实现数据处理扩展插件](../extensions/data-processing/implementing-a-data-processing-extension.md)   
 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)   
 [创建、删除或修改共享数据源（报表管理器）](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [配置报表的数据源属性（报表管理器）](configure-data-source-properties-for-a-report-report-manager.md)  
  
  
