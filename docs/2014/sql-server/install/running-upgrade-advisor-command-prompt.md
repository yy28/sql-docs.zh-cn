---
title: 正在运行升级顾问（命令提示符） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], running
- command prompt [Upgrade Advisor]
- UpgradeAdvisorWizardCmd utility
- XML formats [Upgrade Advisor]
ms.assetid: 7c83049b-9227-4723-9b7f-66288bc6bd1d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 997d637d109c04dbecb3105538f51fa6ece0518f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66092438"
---
# <a name="running-upgrade-advisor-command-prompt"></a>运行升级顾问（命令提示符）
  使用**UpgradeAdvisorWizardCmd**实用工具从命令提示符运行升级顾问。 可以选择以 XML 格式或以逗号分隔值文件来接收结果。  
  
## <a name="syntax"></a>语法  
  
```  
  
      UpgradeAdvisorWizardCmd [ -? ]  |   
    [ -ConfigFilefilename | <server_info> ]  
    [ -SqlUserlogin_id-SqlPasswordpassword ]  
    [ -CSV ]  
  
where <server_info> is any combination of the following:  
        -Serverserver_name-Instanceinstance_name-ASInstanceAS_instance_name-RSInstanceRS_instance_name  
```  
  
## <a name="arguments"></a>参数  
 **-?**  
 显示命令的语法。  
  
 **-Read-configfile** _filename_  
 XML 文件的路径名和文件名，其中包含运行**UpgradeAdvisorWizardCmd**实用程序时要使用的设置。  
  
 *<server_info>*  
 指定要分析的计算机和实例。 如果不使用配置文件，则使用这些选项。  
  
 *<server_info>* 可以是以下四个参数的任意组合：  
  
 **-服务器** _server_name_  
 指定要分析的计算机的名称。 这可以是本地计算机（默认值）或远程计算机。  
  
 **-Instance** _instance_name_  
 指定要分析的实例的名称。 没有默认值。 如果未指定此参数， [!INCLUDE[ssDE](../../includes/ssde-md.md)]则不会扫描。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的默认实例的值是 MSSQLSERVER。 对于命名实例，使用实例名称。  
  
 **-ASInstance**  _AS_instance_name_  
 指定要分析的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的名称。 没有默认值。 如果不指定此值，则不会扫描 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]。 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 默认实例的值是 MSSQLServerOLAPService。 对于命名实例，使用实例名称。  
  
 **-RSInstance**  _RS_instance_name_  
 指定要分析的 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 实例的名称。 没有默认值。 如果不指定此值，则不会扫描 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。 
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 默认实例的值是 ReportServer。 对于命名实例，使用实例名称。  
  
 **-SqlUser** _login_id_  
 如果使用的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则此值是升级顾问将用于连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 如果不指定登录名，则使用 Windows 身份验证连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
 **-SqlPassword** _密码_  
 如果使用 **-SqlUser**参数，请使用此参数指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名的密码。  
  
 **-CSV**  
 指定除了标准 XML 结果外还将结果以逗号分隔值写入到 .csv 文件中。 结果将写入 "我的文档\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] " 升级 Advisor\110\Reports 文件夹中。  
  
## <a name="return-values"></a>返回值  
 下表显示**UpgradeAdvisorWizardCmd**返回的值。  
  
|值|说明|  
|-----------|-----------------|  
|0|成功完成分析，找不到任何升级问题。|  
|正整数|成功完成分析，找到升级问题。|  
|负整数|分析失败。|  
  
## <a name="remarks"></a>备注  
 可在一个 XML 配置文件中提供运行分析所需的所有信息（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证用户名和密码除外）。 此 XML 配置文件记录在模板中。 如果不使用配置文件，则可以通过指定计算机名和实例名使用默认设置分析 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例中所有安装的组件。 有关默认配置文件设置的说明，请参阅本主题后面的“元素说明”表。  
  
## <a name="configuration-file-template"></a>配置文件模板  
 可使用以下 XML 作为模板来创建自己的配置文件。 您可以修改模板，以满足组织的需要。  
  
```xml  
<Configuration>  
    <Server> </Server>  
    <Instance></Instance>  
    <Components>  
        <SQLServer>  
            <Databases>  
                <Database></Database>  
            </Databases>  
            <TraceFiles>  
                <TraceFile></TraceFile>  
            </TraceFiles>  
            <BatchFiles>  
                <BatchFile></BatchFile>  
            </BatchFiles>  
            <BatchSeparator></BatchSeparator>  
        </SQLServer>  
        <AnalysisServices>  
            <ASInstance></ASInstance>  
            <Databases>  
                <Database></Database>  
            </Databases>  
        </AnalysisServices>  
        <ReportingServices>  
            <RSInstance></RSInstance>  
        </ReportingServices>  
        <IntegrationServices>  
            <PackagePath></PackagePath>  
        </IntegrationServices>  
    </Components>  
</Configuration>  
```  
  
## <a name="element-descriptions"></a>元素说明  
  
|标记|定义|出现次数|  
|---------|----------------|----------------|  
|`Configuration`|升级顾问配置文件的父元素。|每个配置文件必须出现一次。|  
|`Server`|要分析的服务器的名称。|每个配置文件可以出现一次。 默认值为本地计算机。|  
|`Instance`|要分析的[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的名称。|每个配置文件可以出现一次。 默认值为默认实例。<br /><br /> 如果服务器上存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元素或 `IntegrationServices` 元素，则每个配置文件必须出现一次。|  
|`Components`|包含指定要分析的组件的元素。|每个配置文件必须出现一次。|  
|`SQLServer`|包含[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例的分析设置。|每个配置文件可以出现一次。 如果未指定，则不会分析 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 数据库。|  
|
  `Databases` 元素的 `SQLServer`|包含要分析的数据库的列表。|对于每个`SQLServer`元素是可选的。 如果此元素不存在，则分析实例中的所有数据库。|  
|
  `Database` 元素的 `SQLServer`|指定要分析的数据库的名称。|如果 `Databases` 元素存在，则必须出现一次或多次。 如果 `Database` 元素包含值“*”，则分析实例中的所有数据库。 没有默认值。|  
|`TraceFiles`|包含要分析的跟踪文件的列表。|对于每个`SQLServer`元素是可选的。|  
|`TraceFile`|指定要分析的跟踪文件的路径和名称。|如果 `TraceFiles` 元素存在，则必须出现一次或多次。 没有默认值。|  
|`BatchFiles`|包含要分析的批处理文件的列表。|对于每个`SQLServer`元素是可选的。|  
|`BatchFile`|指定要分析的批处理文件。 可以是多个文件。|如果 `BatchFiles` 元素存在，则必须出现一次或多次。 没有默认值。|  
|`BatchSeparator`|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 批处理文件中使用的批处理分隔符。|对于每个`SQLServer`元素是可选的。 默认值为 GO。|  
|`AnalysisServices`|包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的分析设置。|每个配置文件可以出现一次。 如果未指定，则不会分析 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。|  
|`ASInstance`|指定实例的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]名称。|每个 `AnalysisServices` 元素必须出现一次。 没有默认值。|  
|
  `Databases` 元素的 `Analysis Services`|包含要分析的数据库的列表。|对于每个`AnalysisServices`元素是可选的。 如果此元素不存在，则分析实例中的所有数据库。|  
|
  `Database` 元素的 `AnalysisServices`|指定要分析的数据库的名称。|如果 `Databases` 元素存在，则必须出现一次或多次。 如果 `Database` 元素包含值“*”，则分析实例中的所有数据库。 没有默认值。|  
|`ReportingServices`|指定对 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 运行分析。|每个配置文件可以出现一次。 如果未指定，则不会分析 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。|  
|`RSInstance`|指定实例的[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]名称。|每个 `ReportingServices` 元素必须出现一次。 没有默认值。|  
|`IntegrationServices`|包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 的分析设置。|每个配置文件可以出现一次。 如果未指定，则不会分析 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]。|  
|`PackagePath`|指定一组 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包的路径。|对于每个`IntegrationServices`元素是可选的。 如果此元素不存在，则[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]会在实例上进行分析，而不会分析外部存储的包。 没有默认值。|  
  
## <a name="examples"></a>示例  
  
### <a name="a-run-upgrade-advisor-using-a-configuration-file"></a>A. 使用配置文件运行升级顾问  
 下面的示例演示如何通过使用指定分析内容的配置文件从命令提示符运行升级顾问。 本例使用 Windows 身份验证连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
```  
UpgradeAdvisorWizardCmd -ConfigFile "C:\My Documents\UpgradeConfig1.xml"  
```  
  
### <a name="b-run-upgrade-advisor-using-default-configuration-settings"></a>B. 使用默认配置设置运行升级顾问  
 下面的示例演示如何通过使用默认配置设置和 Windows 身份验证从命令提示符运行升级顾问。  
  
```  
UpgradeAdvisorWizardCmd -Server MyServer -Instance MyInst   
```  
  
### <a name="c-run-upgrade-advisor-using-includessnoversionincludesssnoversion-mdmd-authentication"></a>C. 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证运行升级顾问  
 下面的示例演示如何通过使用配置文件从命令提示符运行升级顾问。 本例指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户名和密码以连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。  
  
```  
UpgradeAdvisorWizardCmd -ConfigFile "C:\My Documents\UpgradeConfig1.xml"   
    -SqlUser "MyUserName" -SqlPassword "QweRTy-55"  
```  
  
## <a name="see-also"></a>另请参阅  
 [解决升级问题](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [使用升级顾问](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [&#40;用户界面运行升级顾问&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)  
  
  
