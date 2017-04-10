---
title: "Analysis Services 中表格模型的兼容级别 | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.asvs.bidtoolset.versioncompat.f1"
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
caps.latest.revision: 27
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 27
---
# Analysis Services 中表格模型的兼容级别
  模型或数据库的兼容级别是指 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 引擎中一组特定于版本的行为。 可以在任何支持的兼容级别上创建模型，以获取特定版本的行为。 例如，DirectQuery 和表格对象元数据具有不同的实现，具体取决于兼容级别分配。  
  
 **SQL Server 2016 RTM (1200)**（或简称为 1200 兼容级别）是 SQL Server 2016 中的新增部分，仅适用于表格模型。  1200 兼容级别的表格模型将仅在 [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)] 表格实例上运行。  
  
 若要创建或升级表格模型，请使用 SQL Server Data Tools (SSDT)，并在创建项目时设置“兼容级别”属性，或于创建项目后在 **model.bim** 文件中设置。  
  
> [!NOTE]  
>  就兼容级别而言，多维模型遵照独立版本路径。 正如 1103 一样，数字碰巧相同只是一种巧合。 有关详细信息，请参阅[多维数据库的兼容级别 (Analysis Services)](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)。  
  
## 表格模型数据库支持的兼容级别  
 Analysis Services 支持以下兼容级别（适用于模型和数据库）。  用于创建模型的工具版本决定了更高的兼容级别是否可用。  
  
||||  
|-|-|-|  
|兼容级别|服务器版本|建模工具版本|  
|1200|仅在 SQL Server 2016 实例上运行|[仅 Visual Studio 2015 适用的 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>1</sup><br /><br /> [What's New in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md) 描述了此级别可用的功能。|  
|1103|SQL Server 2016<br /><br /> SQL Server 2014<br /><br /> SQL Server 2012 SP1|[适用于 Visual Studio 2015 的 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>2</sup><br /><br /> [SQL Server Data Tools for Business Intelligence (Visual Studio 2013)](https://www.microsoft.com/en-us/download/details.aspx?id=42313)<br /><br /> [SQL Server Data Tools for Business Intelligence (Visual Studio 2012)](http://www.microsoft.com/en-us/download/details.aspx?id=36843)|  
|1100|SQL Server 2016<br /><br /> SQL Server 2014<br /><br /> SQL Server 2012 SP1<br /><br /> SQL Server 2012|[适用于 Visual Studio 2015 的 SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=690931) <sup>1</sup><br /><br /> [SQL Server Data Tools for Business Intelligence (Visual Studio 2013)](https://www.microsoft.com/en-us/download/details.aspx?id=42313)<br /><br /> [SQL Server Data Tools for Business Intelligence (Visual Studio 2012)](http://www.microsoft.com/en-us/download/details.aspx?id=36843)<br /><br /> Business Intelligence Development Studio（在 Visual Studio 2010 Shell 中运行并通过 SQL Server 安装程序安装）|  
  
 <sup>1</sup> 可以使用 SQL Server Data Tools for Visual Studio 2015 为早期版本的 Analysis Services 部署 1100 或 1103 表格模型。  
  
 <sup>2</sup> 兼容级别 1100、1103 和 1200 对于适用于 Visual Studio 2015 的 SQL Server Data Tools 中的表格模型项目均有效，但只能在 Analysis Services 的 SQL Server 2016 实例上部署和运行 1200 模型。  
  
## 在 SSDT 中创建或升级表格时设置兼容级别  
 在 SQL Server Data Tools (SSDT) 中创建新的表格模型项目时，可以在“新建表格项目选项”对话框中指定兼容级别：  
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.jpg "ssas_tabularproject_compat1200")  
  
 您还可以通过选择 **“不再显示此消息”** 选项指定默认的兼容级别。 所有后续项目都将使用您指定的兼容级别。 可以在 SSDT 的“工具” > “选项”中更改默认兼容级别。  
  
 若要升级表格模型项目，可在模型“属性”窗口中将“兼容级别”属性设置为“SQL Server 2016 RTM (1200)”。  有关详细信息，请参阅 [Upgrade Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md) 。  
  
> [!NOTE]  
>  可以基于导入的 Power Pivot 工作簿创建表格模型。 默认情况下，Power BI Desktop 将自动在 1200 兼容级别创建表格模型。 但是，早期版本的 Power Pivot 工作簿可能是 1100 级别。 当使用旧版工作簿时，请记得要更改“兼容级别”  属性以便对其进行升级。  
  
## 检查 SSMS 中数据库的兼容级别  
 在 SSMS 中，右键单击数据库名称，然后选择“属性” > “兼容级别”属性。  
  
## 检查 SSMS 中支持的服务器兼容级别  
 在 SSMS 中，右键单击服务器名称，然后选择“属性” > “支持的兼容级别”。  
  
 此属性指定将在服务器上运行的数据库的最高兼容级别。  支持的兼容级别为只读，无法更改。  
  
## 另请参阅  
 [多维数据库的兼容级别 (Analysis Services)](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Analysis Services 中的新增功能](../../analysis-services/what-s-new-in-analysis-services.md)   
 [从 PowerPivot 导入（SSAS 表格）](../../analysis-services/tabular-models/import-from-power-pivot-ssas-tabular.md)   
 [创建新的表格模型项目 (Analysis Services)](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  