---
title: 分析服务器属性对话框 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- SQL12.ASVS.SSMSIMBI.SERVERPROPERTIES.F1
- SQL12.ASVS.SQLSERVERSTUDIO.SERVERPROPERTIES.F1
helpviewer_keywords:
- Analysis Server Properties dialog box
ms.assetid: b01ec658-c191-49c9-a6cb-549b21a368ab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: afa6c20ccf591b4cea6917cd11817cb24c786abd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078057"
---
# <a name="analysis-server-properties-dialog-box-analysis-services"></a>“分析服务器属性”对话框 (Analysis Services)
  可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的“分析服务器属性”对话框，为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例设置常规、语言/排序规则和安全设置。 通过在“对象资源管理器”中右键单击某个 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例，再从上下文菜单中选择“属性”，可以显示“分析服务器属性”对话框。 **“分析服务器属性”** 对话框包含下列属性。  
  
## <a name="information-properties"></a>信息属性  
 使用此页可查看服务器模式、版本和兼容性级别。 每个实例均在表格或多维服务器模式下进行安装，且能够加载表格或多维模型。 如果您需要支持这两种模式，则必须安装两个实例。  
  
 **支持的兼容级别**等效于`DefaultCompatibilityLevel`AMO 中的属性。 它是只读的，且基于安装期间指定的服务器部署模式。 服务器在执行因服务器模式或版本而异的操作（如将表格数据库的备份还原到表格服务器实例上）时会检查此属性。 请不要将其与表格模型或多维模型的数据库兼容模式混淆，它们具有类似的名称和值。 此服务器属性的有效值包括：  
  
-   对于多维模式和数据挖掘模式，**1100** 是部署模式 0 的默认兼容级别。  
  
-   对于支持表格模式或**的安装，** 1103 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]是部署模式 1 或 2 的默认兼容级别。  
  
 在支持命名空间的客户端请求 DISCOVER_XML_METADATA 时，服务器将返回此值。 有关详细信息，请参阅 [DISCOVER_XML_METADATA 行集](schema-rowsets/xml/discover-xml-metadata-rowset.md)。  
  
## <a name="general-properties"></a>常规属性  
 使用此页可设置 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的基本和高级的常规属性，如文件夹位置和网络设置。  
  
 服务器属性页仅显示管理员更有可能更改的属性，如用于针对特定配置优化服务器的内存和线程池属性。 下面的列表提供了指向主属性组的链接：  
  
-   [常规属性](server-properties/general-properties.md)  
  
-   [数据挖掘属性](server-properties/data-mining-properties.md)  
  
-   [功能属性](server-properties/feature-properties.md)  
  
-   [文件存储属性](server-properties/filestore-properties.md)  
  
-   [锁管理器属性](server-properties/lock-manager-properties.md)  
  
-   [日志属性](server-properties/log-properties.md)  
  
-   [内存属性](server-properties/memory-properties.md)  
  
-   [网络属性](server-properties/network-properties.md)  
  
-   [OLAP 属性](server-properties/olap-properties.md)  
  
-   [安全属性](server-properties/security-properties.md)  
  
-   [线程池属性](server-properties/thread-pool-properties.md)  
  
## <a name="language-collation-properties"></a>语言排序规则属性  
 使用此页可设置 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的默认语言和排序规则选项。 下面的列表包含每个选项的简短说明。 有关更多详细说明，请参阅[语言和排序规则 (Analysis Services)](languages-and-collations-analysis-services.md)。  
  
-   **“二进制”** 用于根据为每个字符定义的位模式对数据进行排序和比较。 二进制排序顺序区分大小写，即先小写字母后大写字母，并区分重音。 这是最快的排序顺序。  
  
     如果未选择此选项，则 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将遵循字典中定义的相关语言或字母表的排序和比较规则。  
  
    > [!NOTE]  
    >  如果选择此选项，将会禁用“区分大小写”、“区分重音”、“区分假名”和“区分全半角”选项。  
  
-   **“二进制 2”** 用于根据为每个字符定义的位模式对 Unicode 数据进行排序和比较。 二进制排序顺序区分大小写，即先小写字母后大写字母，并区分重音。 这是最快的排序顺序。  
  
-   “区分大小写”用于根据为相关语言或字母表提供的字典规则对数据进行排序和比较，并区分大小写字母。  
  
     如果未选择此选项， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将认为大写字母和小写字母是一样的。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不会定义是否排序或字母与大写字母**区分大小写**未选中。  
  
-   “区分重音”用于根据为相关语言或字母表提供的字典规则对数据进行排序和比较，并区分重音和非重音字符。 例如，“a”和“á”将被视为不同的字符。  
  
     如果未选择此选项，则 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 会将字母的重音形式和非重音形式视为相同。  
  
-   “区分假名”用于根据为相关语言或字母表提供的字典规则对数据进行排序和比较，并区分日语中的两种假名字符类型：平假名和片假名。  
  
     如果未选择此选项，则 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 会将平假名字符和片假名字符视为相同。  
  
-   “区分全半角”用于根据为相关语言或字母表提供的字典规则对数据进行排序和比较，并区分以单字节字符（半角）和双字节字符（全角）表示的相同字符。  
  
     如果未选择此选项，则 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 会将同一字符的单字节形式和双字节形式视为相同。  
  
## <a name="security-properties"></a>安全属性  
 使用此页可为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例指定属于服务器管理员角色的 Windows 用户帐户和组帐户。 此角色中的成员身份传达执行服务器范围内任务（如创建或处理数据库、修改服务器属性、添加或删除此角色的其他成员或启动跟踪）的权限。 请参阅[授予服务器管理员权限&#40;Analysis Services&#41; ](instances/grant-server-admin-rights-to-an-analysis-services-instance.md)有关详细信息。  
  
## <a name="see-also"></a>请参阅  
 [确定 Analysis Services 实例的服务器模式](instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [在 Analysis Services 中配置服务器属性](server-properties/server-properties-in-analysis-services.md)   
 [Analysis Services 支持的身份验证方法](instances/authentication-methodologies-supported-by-analysis-services.md)   
 [角色和权限&#40;Analysis Services&#41;](multidimensional-models/roles-and-permissions-analysis-services.md)   
 [语言和排序规则&#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)  
  
  
