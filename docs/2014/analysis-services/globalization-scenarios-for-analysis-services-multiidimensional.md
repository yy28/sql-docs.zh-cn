---
title: Analysis Services Multiidimensional 的全球化方案 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- multiple language support [Analysis Services]
- languages [Analysis Services]
- SSAS, international considerations
- international considerations [Analysis Services]
- global considerations [Analysis Services]
- SQL Server Analysis Services, international considerations
- Analysis Services, international considerations
ms.assetid: e8af85ff-ef33-4659-a003-bb34578eb2a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eb6f1072396b957dc9d4b1e9b7d1089e30c739c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080891"
---
# <a name="globalization-scenarios-for-analysis-services-multiidimensional"></a>Analysis Services Multidimensional 的全球化方案
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在表格数据模型和多维数据模型中存储和操作多语言数据和元数据。 数据以 Unicode (UTF-16) 格式存储为使用 Unicode 编码的字符集。 如果将 ANSI 数据加载进一个数据模型，字符会使用 Unicode 等效码位进行存储。  
  
 Unicode 支持的意义意味着 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 可以 Windows 客户端和服务器操作系统支持的任何语言存储数据，允许在 Windows 计算机上使用的任意字符集中读取、写入、比较数据和对数据进行排序。 占用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据的 BI 客户端应用程序能以用户选择的语言表示数据（假定数据在模型中以那种语言形式存在）。  
  
 语言支持对不同的人有不同的含义。 以下列表回答了几个有关 Analysis Services 如何支持语言的常见问题。  
  
-   如之前所述，数据存储在 Windows 客户端操作系统上的 Unicode 编码字符集中。  
  
-   元数据（如对象名、标识符和说明）也可以为任何 Unicode 语言和脚本形式。 即使工具和环境使用的是另一种语言仍是如此。 例如，在整个堆栈中使用英语和拉丁语排序规则的开发环境中，你可以在你的模型中包含一个名称中使用了西里尔语字符的对象。  
  
     标题和属性成员能用翻译表示（仅适用于多维模型）。 你可以定义一个或多个翻译，然后使用区域设置标识符来决定向客户端返回哪个翻译。 请参阅下方的 [功能](#bkmk_features) ，了解更多信息。  
  
-   从 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 引擎 (msmdsrv) 返回的错误、警告和信息性消息本地化为 Office 和 Office 365 支持的 43 种语言。 无需配置即可获得特定语言的消息。 客户端应用程序的区域设置决定了返回哪些字符串。  
  
-   配置文件 (msmdsrv.ini) 和 AMO PowerShell 仅为英文形式。  
  
-   假定你已经在运行 Analysis Services 的 Windows 服务器上安装了语言包，日志文件将包含英语消息和本地化消息的混合消息。  
  
-   文档和工具，如[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]和[!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)]，翻译成这些语言：简体中文、 繁体中文、 法语、 德语、 意大利语、 日语、 朝鲜语、 葡萄牙语 （巴西）、 俄语和西班牙语。 若要使用特定语言版本的工具，请安装特定语言版本的 SQL Server（例如，安装德语版本的 SQL Server 以获得德语的 Management Studio）或在 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)]的目标语言中运行独立安装。  
  
 Analysis Services 能让你在整个对象层次结构中单独设置语言、排序规则和翻译。  
  
 通过语言、排序规则和翻译实现的方案包括：  
  
-   一个数据模型提供多个翻译后的标题，这样字段名和值就会以用户选择的语言显示。 对于在双语国家/地区运营的公司（如加拿大、比利时或瑞士），在客户端和服务器应用程序中支持多语言是标准编码要求。 此方案通过翻译和货币换算来实现。 参见下方的 [功能](#bkmk_features) 了解详细信息和链接。  
  
-   开发和生产环境在地理上位于不同国家。 在一个国家/地区开发一个解决方案然后将其部署到另一个国家/地区的情况越来越常见。 如果你的任务是准备将以一种语言开发的解决方案部署到使用另一种语言包的服务器上，了解如何设置语言和排序规则属性是十分必要的。 设置这些属性让你能够覆盖从原始主机系统继承的默认设置。 有关详细信息，请参阅下方的 [语言和排序规则 (Analysis Services)](languages-and-collations-analysis-services.md) 。  
  
##  <a name="bkmk_features"></a> 用于生成全球化多维解决方案的功能  
 仅 [!INCLUDE[applies](../includes/applies-md.md)] 多维数据模型  
  
 在客户端级别，使用和操作 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多维数据的全球化应用程序可以使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]中的多语言和多文化功能：  
  
-   [翻译&#40;Analysis Services&#41; ](translations-analysis-services.md)用于嵌入多个标题为单个对象，其中每个已翻译的字符串可以与其他翻译同时存在。 你可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 定义多维数据集、度量值、维度和属性的标题、说明和账户类型的翻译。 您可以检索已为其自动定义了翻译（通过在连接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例时提供区域设置标识符）的 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象的数据和元数据。  
  
     有关如何使用此功能可在[第 9 课：定义透视和翻译](lesson-9-defining-perspectives-and-translations.md)的[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]教程。  
  
-   [货币换算&#40;Analysis Services&#41; ](currency-conversions-analysis-services.md)是通过专用 MDX 脚本转换包含货币数据的度量值。 你可以使用 [!INCLUDE[ss_dtbi](../includes/ss-dtbi-md.md)] 中的商业智能向导生成一个 MDX 脚本，它使用来自维度、属性和度量值组的组合数据与元数据来转换包含货币数据的度量值。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[语言和排序规则 (Analysis Services)](languages-and-collations-analysis-services.md)|为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例指定默认语言和 Windows 排序规则。 你的选择会影响由 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]管理的数据和元数据。|  
|[翻译&#40;Analysis Services&#41;](translations-analysis-services.md)|定义 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库的翻译和该数据库包含的对象的翻译。 本主题说明了 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 如何解析客户端应用程序对翻译的数据与元数据的请求。|  
|[货币换算&#40;Analysis Services&#41;](currency-conversions-analysis-services.md)|使用商业智能向导定义货币换算。|  
|[全球化提示和最佳实践 (Analysis Services)](globalization-tips-and-best-practices-analysis-services.md)|查看几个能帮助你避免有关多语言数据的问题的设计和编码实践。|  
  
## <a name="see-also"></a>请参阅  
 [Windows 应用程序的国际化](/windows/desktop/Intl/international-support)   
 [Microsoft 全球化文档](/globalization/)   
 [使用基于区域设置的自适应设计编写 Windows 应用商店应用](http://blogs.windows.com/buildingapps/2014/03/06/writing-windows-store-apps-with-locale-based-adaptive-design/)   
 [使用 C# 和 XAML 开发通用 Windows 应用](http://www.microsoftvirtualacademy.com/training-courses/developing-universal-windows-apps-with-c-and-xaml)  
  
  
