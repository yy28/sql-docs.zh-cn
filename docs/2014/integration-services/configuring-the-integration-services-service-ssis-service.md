---
title: 配置 Integration Services 服务 （SSIS 服务） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Integration Services service, configuring
- configuration files [Integration Services]
- service [Integration Services], configuring
- default configuration files
ms.assetid: 36d78393-a54c-44b0-8709-7f003f44c27f
caps.latest.revision: 70
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 71a0436edf57e820b7e6b559814f65823d4390eb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37283673"
---
# <a name="configuring-the-integration-services-service-ssis-service"></a>配置 Integration Services 服务（SSIS 服务）
    
> [!IMPORTANT]  
>  本主题论述 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务，该服务是用于管理 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包的一种 Windows 服务。 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)] 支持该服务以便与 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的早期版本向后兼容。 从 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]开始，您可以在 Integration Services 服务器上管理诸如包之类的对象。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务使用某个配置文件中的设置。 默认情况下，此配置文件的名称为 MsDtsSrvr.ini.xml，并且该文件位于文件夹 %ProgramFiles%\Microsoft SQL Server\120\DTS\Binn 中。  
  
 通常，您不必对此配置文件进行任何更改，也不必更改文件的默认位置。 但是，如果包存储在 [!INCLUDE[ssDE](../includes/ssde-md.md)]的某个命名实例或远程实例中，或存储在 [!INCLUDE[ssDE](../includes/ssde-md.md)]的多个实例中，则必须修改该配置文件。 此外，如果您将配置文件移到默认位置之外的位置，则必须修改指定该文件位置的注册表项。  
  
## <a name="configuration-file-contents"></a>配置文件内容  
 安装 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]时，安装过程会创建并安装 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务的配置文件。 此配置文件包含以下设置：  
  
-   服务停止时将向包发送停止命令。  
  
-   在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 的对象资源管理器中为 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 显示的根文件夹是 MSDB 和“文件系统”文件夹。  
  
-   文件系统中的包的[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]服务管理位于 %ProgramFiles%\Microsoft SQL Server\120\DTS\Packages 中。  
  
 此配置文件还指定哪个 msdb 数据库包含将由 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务管理的包。 默认情况下， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务配置为管理 [!INCLUDE[ssDE](../includes/ssde-md.md)] 实例的 msdb 数据库中的包，该实例与 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]同时安装。 如果未同时安装 [!INCLUDE[ssDE](../includes/ssde-md.md)] 实例，则 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务可配置为管理本地默认 [!INCLUDE[ssDE](../includes/ssde-md.md)]实例的 msdb 数据库中的包。  
  
### <a name="default-configuration-file-example"></a>默认配置文件示例  
 下面的示例显示了指定以下设置的默认配置文件：  
  
-   当 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务停止时包停止运行。  
  
-   包存储的根文件夹在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中为 MSDB 和“文件系统”。  
  
-   该服务管理存储在本地默认 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例的 msdb 数据库中的包。  
  
-   该服务管理存储在文件系统的“包”文件夹中的包。  
  
 **默认配置文件示例**  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    <Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>.</ServerName>  
    </Folder>  
    <Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
## <a name="modification-of-the-configuration-file"></a>配置文件的修改  
 可以通过修改配置文件来达到以下目的：允许包在服务停止时继续运行；在对象资源管理器中显示其他根文件夹；或者指定文件系统中的一个不同文件夹或其他文件夹由 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务进行管理。 例如，可以创建 `SqlServerFolder` 类型的其他根文件夹来管理其他[!INCLUDE[ssDE](../includes/ssde-md.md)]实例的 msdb 数据库中的包。  
  
> [!NOTE]  
>  某些字符在文件夹名称中无效。 文件夹名称的有效字符由 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 类 **System.IO.Path** 和 **GetInvalidFilenameChars** 字段决定。 **GetInvalidFilenameChars** 字段提供了不能在传递给 **Path** 类成员的路径字符串参数中指定的特定于平台的字符数组。 无效的字符集会因文件系统的不同而不同。 通常，无效字符为引号 (")、小于号 (<) 字符和竖线 (|) 字符。  
  
 但是，您必须修改配置文件，才能管理存储在 [!INCLUDE[ssDE](../includes/ssde-md.md)]的某个命名实例或远程实例中的包。 如果不更新配置文件，则无法在 **中使用** 对象资源管理器 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 来查看存储在该命名实例或远程实例的 msdb 数据库中的包。 如果尝试使用 **对象资源管理器** 查看这些包，将收到以下错误消息：  
  
 `Failed to retrieve data for this request. (Microsoft.SqlServer.SmoEnum)`  
  
 `The SQL Server specified in Integration Services service configuration is not present or is not available. This might occur when there is no default instance of SQL Server on the computer. For more information, see the topic "Configuring the Integration Services Service" in SQL Server 2008 Books Online.`  
  
 `Login Timeout Expired`  
  
 `An error has occurred while establishing a connection to the server. When connecting to SQL Server 2008, this failure may be caused by the fact that under the default settings SQL Server does not allow remote connections.`  
  
 `Named Pipes Provider: Could not open a connection to SQL Server [2]. (MsDtsSvr).`  
  
 若要修改 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务的配置文件，可使用文本编辑器。  
  
> [!IMPORTANT]  
>  修改了服务配置文件后，必须重新启动该服务才能使用更新后的服务配置。  
  
### <a name="modified-configuration-file-example"></a>经过修改的配置文件示例  
 下面的示例显示了经过修改的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]配置文件。 此文件用于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 命名实例 `InstanceName` ，该实例在 `ServerName`服务器上。  
  
 **经过修改的 SQL Server 命名实例配置文件的示例**  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<DtsServiceConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <StopExecutingPackagesOnShutdown>true</StopExecutingPackagesOnShutdown>  
  <TopLevelFolders>  
    <Folder xsi:type="SqlServerFolder">  
      <Name>MSDB</Name>  
      <ServerName>ServerName\InstanceName</ServerName>  
    </Folder>  
    <Folder xsi:type="FileSystemFolder">  
      <Name>File System</Name>  
      <StorePath>..\Packages</StorePath>  
    </Folder>  
  </TopLevelFolders>    
</DtsServiceConfiguration>  
```  
  
## <a name="modification-of-the-configuration-file-location"></a>配置文件位置的修改  
注册表项**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS\ServiceConfigFile**指定文件的位置和配置名称[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]服务使用。 注册表项的默认值是**C:\Program Files\Microsoft SQL Server\120\DTS\Binn\MsDtsSrvr.ini.xml**。 可以更新该注册表项的值，以使配置文件使用其他名称和位置。 请注意，在路径中的版本号 (适用于 SQL Server 的 120 [!INCLUDE[ssSQL14_md](../includes/sssql14-md.md)]) 将 SQL Server 版本而异。 
  
  
> [!CAUTION]  
>  如果注册表编辑不当，可能会导致严重问题并需要重新安装操作系统。 [!INCLUDE[msCoName](../includes/msconame-md.md)] 不能保证可以解决因注册表编辑不当的问题。 编辑注册表之前，请备份所有重要数据。 有关如何备份、还原和编辑注册表的信息，请参阅 [!INCLUDE[msCoName](../includes/msconame-md.md)] 知识库文章 [Microsoft Windows 注册表说明](http://support.microsoft.com/kb/256986)。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服务在启动时加载配置文件。 对注册表项进行任何更改都需要重新启动服务。  
  
  
