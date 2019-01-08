---
title: 重大更改 Analysis Services SQL Server 2014 中的功能 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- breaking changes [Analysis Services]
- upgrading Analysis Services
ms.assetid: aeb02542-5a6c-458c-a110-13413dd3e9d9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 944385d23b39938a6cb4a28afa16c3d2d67dca23
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52391990"
---
# <a name="breaking-changes-to-analysis-services-features-in-sql-server-2014"></a>SQL Server 2014 中 Analysis Services 功能的重大更改
  本主题介绍 [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]中的重大更改。 这些更改可能导致基于 SQL Server 早期版本的应用程序、脚本或功能无法继续使用。  
  
 本主题内容：  
  
-   [SQL Server 2014 中的重大更改](#bkmk_sql2014)  
  
-   [SQL Server 2012 SP1 中的重大更改](#bkmk_2012Sp1)  
  
-   [SQL Server 2012 中的重大更改](#bkmk_sql11)  
  
-   [SQL Server 2008/SQL Server 2008 R2 中的重大更改](#bkmk_sql10)  
  
##  <a name="bkmk_sql2014"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 中的重大更改  
 此版本中，没有针对表格、多维、数据挖掘或 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 功能的新的重大更改。  但是，由于  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] 非常类似于 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 和 [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] 版本，因而如果你要从 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]进行升级，为方便起见，此处提供了这两个以前版本的重大更改。  
  
##  <a name="bkmk_2012Sp1"></a> SQL Server 2012 SP1 中的重大更改  
 已经知道与全球化相关的代码更改会破坏某些应用程序。 已知问题包括：  
  
 **对象标识符区分大小写**  
 旨在使所有对象标识符不区分大小写的代码更改对某些语言会产生相反的影响。 目的是所有对象标识符将不区分大小写，不管选择的是哪种排序规则。 此更改使 Analysis Services 与同一解决方案堆栈中通常所使用的其他应用程序相一致。  
  
 对于基于基本拉丁字母表的 26 个字符的语言，对象标识符现在不区分大小写，这是预期的行为。  
  
 对于西里尔文和其他使用大小写格式的双语言脚本（希腊语、亚美尼亚语和科普特语），对象标识符现在区分大小写。 当对象标识符和其引用方式之间存在大小写区别时（例如，引用所有小写对象标识符的处理脚本），最可能发生重大更改。 此行为有可能在将来发生变化，但作为一种临时的解决方法，我们建议修改脚本，使用与对象标识符相同的大小写。  
  
##  <a name="bkmk_sql11"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中的重大更改  
 本节介绍针对 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中的 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]功能报告的重大更改。  
  
|问题|Description|  
|-----------|-----------------|  
|删除了针对 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 安装的安装命令。|安装程序安装但不再配置 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]。 现在删除了用于为配置操作收集值的安装命令。 这些安装命令包括 /FARMACCOUNT、/FARMPASSWORD、/PASSPHRASE 和 /FARMADMINPORT。<br /><br /> 如果您为无人参与的安装创建了安装脚本，将需要针对 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] 安装修改这些脚本。 方法之一是使用 PowerShell cmdlet 将服务器配置为无人参与模式。 有关详细信息，请参阅[从命令提示符安装 PowerPivot](../../2014/sql-server/install/install-powerpivot-from-the-command-prompt.md)并[使用 Windows PowerShell 配置 PowerPivot](power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)。|  
  
##  <a name="bkmk_sql10"></a> 中的重大更改 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]/[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
 本部分包含先前版本中的重大更改。 如果您从 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]进行升级，则应查看 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 和 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]中引入的重大更改。  
  
|问题|Description|  
|-----------|-----------------|  
|shallow exists 函数与包含枚举成员或枚举集叉积的命名集结合使用的方式已更改。|在 [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]中，shallow exists 函数不可用于包含枚举成员或枚举集叉积的命名集。 若要实现与 [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]的原始发布版本和 SP1 的向后兼容，可将配置属性 ConfigurationSettings\OLAP\Query\NamedSetShallowExistsMode 设置为 1；若要实现与 [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] SP2 的向后兼容，则应将其设置为 2。|  
|VBA 函数对 Null 值和空值的处理方式与 [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] 中的方式有所不同。|在 [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]中，如果将 Null 值或空值用作参数，VBA 函数将返回 0 或空字符串。 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]中，它们将返回 Null。|  
|迁移向导将因默认情况下不安装 DSO 而失败。|默认情况下，SQL Server 2008 不会安装 DSO（决策支持对象）向后兼容组件。 默认情况下将安装向后兼容包，但将禁用该包的 DSO 组件。 由于 SQL Server Analysis Services 迁移向导依赖此组件，因此在未安装该组件的情况下该迁移向导将失败。 若要安装 DSO 组件，请执行下列操作：<br /><br /> 1） 打开控制面板。<br />2） 在 Windows XP 或 Windows Server 2003 中，选择**添加或删除程序**。 在 Windows Vista 和 Windows Server 2008 中，选择 **“程序和功能”**。<br />3） 右键单击**Microsoft SQL Server 2005 向后兼容性**，然后选择**更改**。<br />4） 在向后兼容安装向导中，单击**下一步**。<br />5） 在程序维护页上，选择**修改**，然后单击**下一步**。<br />6） 在功能选择页上，如果决策支持对象 (DSO) 不可用，请单击向下箭头并选择**此功能将安装在本地硬盘上**。 单击“下一步” 。<br />7） 上已准备好修改程序页上，单击**安装**。<br />8） 完成安装后，单击**完成**。<br /><br /> <br /><br /> 迁移已完成的上一步骤后，您可以删除 DSO 到 DSO 的选项更改"**此功能将不可用**。"<br /><br /> 如果未安装向后兼容包，则可以从 SQL Server 2008 分发介质进行安装。 请注意，存在针对各目标体系结构的版本 (x86、x64、ia64)。 可在以下位置找到这些版本：<br /><br /> x86\Setup\x86\SQLServer2005_BC.msi<br /><br /> x64\Setup\x64\SQLServer2005_BC.msi<br /><br /> ia64\Setup\ia64\SQLServer2005_BC.msi|  
|不建议将分区位置放置在 Data 文件夹中。|服务器管理 Data 文件夹，并将在创建、删除和更改对象时创建或删除相应文件夹。 因此，强烈建议不要在 Data 文件夹内指定分区存储位置，尤其是不要在数据库、多维数据集和维度的子文件夹中指定。 尽管服务器允许您使用 Create 或 Alter 命令来执行此操作，但它会显示警告。 如果您将 Data 文件夹中包含有分区存储位置的数据库从 SQL Server 2005 Analysis Services 升级到 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Analysis Services，则此升级操作将成功完成。 还原或同步操作将需要您将分区存储位置移出 Data 文件夹。|  
|您可能会从在 ProClarity Analytics Server 和 Microsoft Office PerformancePoint Server 2007 中使用“EXISTING”MDX 关键字的查询获得意外结果。|某些情况下，ProClarity Analytics Server 和 Microsoft Office PerformancePoint Server 2007 会在 MDX 中错误地使用 EXISTING 关键字。 由于已对 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Analysis Services 进行了更改，因此这些查询可能会返回意外结果。|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 向后兼容性](analysis-services-backward-compatibility.md)  
  
  
