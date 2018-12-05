---
title: 在 SharePoint 集成模式下针对 Reporting Services 启用和禁用 RDL 沙盒 | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 183d7272049c7981a8a3f53a811087866c05c666
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52412744"
---
# <a name="enable-and-disable-rdl-sandboxing-for-reporting-services-in-sharepoint-integrated-mode"></a>在 SharePoint 集成模式下针对 Reporting Services 启用和禁用 RDL 沙盒

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

通过 RDL（报表定义语言）沙盒处理功能，可以在多个租户使用报表服务器的单个 Web 场的情况下检测到和限制单个租户使用特定类型的资源。 相关的示例是宿主服务方案，在此方案中，您可能维护多个用户（并且可能是不同的公司）使用的报表服务器的单个 Web 场。 作为报表服务器管理员，您可以启用此功能以帮助实现以下目标：  
  
-   限制外部资源的大小。 外部资源包括图像、.xslt 文件和地图数据。  
  
-   在报表发布时，限制在表达式文本中使用的类型和成员。  
  
-   在报表处理时，限制文本长度和表达式返回值的大小。

> [!NOTE]
> 自 SQL Server 2016 之后，不再提供 Reporting Services 与 SharePoint 的集成这一功能。

 在启用 RDL 沙盒处理时，禁用以下功能：  
  
-   报表定义的 \<Code> 元素中的自定义代码。  
  
-   用于 [!INCLUDE[ssRSversion2005](../../includes/ssrsversion2005-md.md)] 自定义报表项的 RDL 向后兼容模式。  
  
-   表达式中的命名参数。  
  
 本主题介绍 RSReportServer.Config 文件中 \<RDLSandboxing> 元素内的各元素。 有关如何修改此文件的详细信息，请参阅[修改 Reporting Services 配置文件 (RSreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)。 服务器跟踪日志记录与 RDL 沙盒处理功能相关的活动。 有关跟踪日志的详细信息，请参阅 [报表服务器服务跟踪日志](../../reporting-services/report-server/report-server-service-trace-log.md)。  
  
## <a name="example-configuration"></a>配置示例
 下面的示例显示了 RSReportServer.Config 文件中 \<RDLSandboxing> 元素的设置和示例值。  
  
```  
<RDLSandboxing>  
   <MaxExpressionLength>5000</MaxExpressionLength>  
   <MaxResourceSize>5000</MaxResourceSize>  
   <MaxStringResultLength>3000</MaxStringResultLength>  
   <MaxArrayResultLength>250</MaxArrayResultLength>  
   <Types>  
      <Allow Namespace="System.Drawing" AllowNew="True">Bitmap</Allow>  
      <Allow Namespace="TypeConverters.Custom" AllowNew="True">*</Allow>  
   </Types>  
   <Members>  
      <Deny>Format</Deny>  
      <Deny>StrDup</Deny>  
   </Members>  
</RDLSandboxing>  
```

## <a name="configuration-settings"></a>配置设置

 下表提供了有关配置设置的信息。 将按设置在配置文件中的显示顺序依次列出：  
  
|设置|描述|  
|-------------|-----------------|  
|**MaxExpressionLength**|RDL 表达式中允许的最大字符数。<br /><br /> 默认值：1000|  
|**MaxResourceSize**|外部资源允许的最大 KB 数。<br /><br /> 默认值：100|  
|**MaxStringResultLength**|RDL 表达式的返回值中允许的最大字符数。<br /><br /> 默认值：1000|  
|**MaxArrayResultLength**|RDL 表达式的数组返回值中允许的最大项数。<br /><br /> 默认值：100|  
|**类型**|在 RDL 表达式内允许的成员的列表。|  
|**Allow**|RDL 表达式中允许的一个类型或一组类型。|  
|**Namespace**|**Allow** 的属性，它是包含应用于 Value 的一个或多个类型的命名空间。 此属性不区分大小写。|  
|**AllowNew**|Allow 的布尔属性，控制是否允许在 RDL 表达式中或 RDL \<Class> 元素中创建该类型的新实例。<br /><br /> 在启用 RDLSandboxing 时，无论 AllowNew 的设置如何，都不能在 RDL 表达式中创建新数组。|  
|**ReplTest1**|**Allow** 的值，作为在 RDL 表达式中要允许的类型的名称。 值 **\*** 指示命名空间中的所有类型都是允许的。 此属性不区分大小写。|  
|**成员**|对于在类型 \<Types> 元素中包括的类型的列表，为在 RDL 表达式中不允许的成员名称的列表。|  
|**拒绝**|在 RDL 表达式中不允许的成员的名称。 此属性不区分大小写。<br /><br /> 在为某一成员指定了 Deny 后，不允许所有类型的具有此名称的所有成员。|  
  
## <a name="working-with-expressions-when-rdl-sandboxing-is-enabled"></a>当启用 RDL 沙盒处理时使用表达式

您可以修改 RDL 沙盒处理功能，以便通过以下方式管理表达式使用的资源：  
  
-   限制用于表达式的字符数。  
  
-   限制表达式所返回的结果的大小。  
  
-   允许可以在表达式中使用的类型的特定列表。  
  
-   对于可在表达式中使用的允许类型的列表，按名称限制成员的列表。  
  
-   通过 RDL 沙盒处理功能，您可以创建已批准类型的列表和拒绝的成员的列表。 已批准类型的列表称为允许列表。 拒绝的成员的列表称为阻止列表。  
  
> [!NOTE]  
>  在报表定义中，计算机无法知道表达式引用的每个实例的类型。 在您将一个成员添加到该阻止列表时，即拒绝允许列表中所有类型的该名称的所有成员。  
  
 在运行时验证 RDL 表达式结果。 在发布报表时在报表定义中验证 RDL 表达式。 监控报表服务器跟踪日志以发现冲突。 有关详细信息，请参阅 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)。  
  
### <a name="working-with-types"></a>使用类型

 在您将某一类型添加到允许列表中时，即控制用于访问 RDL 表达式的以下入口点：  
  
-   某一类型的静态成员。  
  
-    [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] **New** 方法。  
  
-   报表定义中的 \<Classes> 元素。  
  
-   已为允许列表中的某一类型添加到阻止列表中的成员。  
  
 允许列表不控制以下入口点：  
  
-   报表数据集。 从查询返回的报表数据集中的字段可以包含任何有效的 RDL 类型。  
  
-   报表参数。 用户提供的参数值可以包含任何有效的 RDL 类型。  
  
-   未处于阻止列表中的已启用类型的成员。 默认情况下，启用允许列表中所有类型的所有成员。 在您将一个成员名称添加到该阻止列表时，即拒绝允许列表中所有类型的具有该名称的所有成员。  
  
 若要启用一种类型的成员，但拒绝其他类型的具有相同名称的成员，必须执行以下操作：  
  
-   为成员名称添加 \<Deny> 元素。  
  
-   对于您想要启用的成员，为其创建一个代理成员，该成员在自定义程序集中的类上具有不同的名称。  
  
-   将该新类添加到允许列表中。  
  
 若要将 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework 函数添加到允许列表，请将来自 Microsoft.VisualBasic 命名空间的相应类型添加到该允许列表。  
  
 若要将 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework 类型关键字添加到允许列表，请将相应的 CLR 类型添加到该允许列表。 例如，若要使用 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework 关键字 Integer，请将以下 XML 片段添加到 \<RDLSandboxing> 元素：  
  
```  
<Allow Namespace="System">Int32</Allow>  
```  
  
 若要将泛型或 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework 可以为 Null 类型添加到允许列表，必须执行以下操作：  
  
-   为泛型或 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework 可以为 Null 类型创建代理类型。  
  
-   向允许列表中添加该代理类型。  
  
 将一个类型从某一自定义程序集添加到允许列表并不隐式授予对该程序集的执行权限。 您必须专门修改代码访问安全文件，并对您的程序集提供执行权限。 有关详细信息，请参阅 [Code Access Security in Reporting Services](../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md)。  
  
#### <a name="maintaining-the-deny-list-of-members"></a>维护成员的 \<Deny> 列表

 在您将某一新类型添加到允许列表时，使用以下列表可以确定何时可能必须更新成员的阻止列表：  
  
-   在您使用引入新类型的版本更新自定义程序集时。  
  
-   在您向允许列表中的类型添加成员时。  
  
-   在您更新报表服务器上的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 时。  
  
-   在您将报表服务器升级到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的更高版本时。  
  
-   在您更新报表服务器以处理更高版本的 RDL 架构时，因为新成员可能已添加到 RDL 类型中。  
  
### <a name="working-with-operators-and-new"></a>使用运算符和 New

 默认情况下，始终允许 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] New **以外的所有**.NET Framework 语言运算符。 New 运算符由 \<Allow> 元素上的 AllowNew 属性控制。 始终允许其他语言运算符（如默认集合取值函数运算符 **!**） 和 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET Framework 转换宏（如 **CInt**）。  
  
 不支持将运算符添加到阻止列表（包括自定义运算符）。 要排除某一类型的运算符，必须执行以下操作：  
  
-   创建一个代理类型，它不实现您想要排除的运算符。  
  
-   向允许列表中添加该代理类型。  
  
 若要在 RDL 表达式中创建一个新数组，请在方法中对您定义的类创建该数组，并且将该类添加到允许列表。  
  
 若要在 RDL 表达式中创建一个新数组，必须执行以下操作：  
  
-   定义一个新类，并在方法中对该类创建数组。  
  
-   将该类添加到允许列表中。  
  
## <a name="see-also"></a>另请参阅

 [RsReportServer.config 配置文件](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [报表服务器服务跟踪日志](../../reporting-services/report-server/report-server-service-trace-log.md)  

更多疑问？ [请访问 Reporting Services 论坛](https://go.microsoft.com/fwlink/?LinkId=620231)
