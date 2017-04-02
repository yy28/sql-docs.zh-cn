---
title: "SQL Server 2016 各个版本支持的 Analysis Services 功能 | Microsoft Docs"
ms.custom: ""
ms.date: "09/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
  - "analysis-services/multidimensional-tabular"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f09d7be1-bd63-43f8-b91c-bf19166b4457
caps.latest.revision: 4
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 3
---
# SQL Server 2016 各个版本支持的 Analysis Services 功能
本主题提供有关不同版本的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]所支持的功能的详细信息。  
  
 可在 180 天的试用期内使用 SQL Server 评估版。  
  
 有关最新的发行说明，请参阅 [SQL Server 2016 Release Notes](../sql-server/sql-server-2016-release-notes.md)。 有关新增功能的最新信息，请参阅 [Analysis Services 中的新增功能](../analysis-services/what-s-new-in-analysis-services.md)。
    
 **试用 SQL Server 2016！**    
    
 > [![从评估中心下载](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[从评估中心下载 SQL Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Azure 虚拟机小](../analysis-services/media/azure-virtual-machine-small.png) **[启动已安装 SQL Server 2016 的虚拟机](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    
    
  
 有关评估版和开发人员版支持的功能，请参阅 SQL Server 企业版。
  
 若要导航到 SQL Server 某种技术相应的表，请单击其链接： 
 
 -  [Analysis Services](#SSAS)  
  
-   [BI 语义模型（多维）](#BIMD)  
  
-   [BI 语义模型（表格）](#BIT)  
  
-   [Power Pivot for SharePoint](#PPSP)  
  
-   [数据挖掘](#DM)  
  
-   [Business Intelligence 客户端](#BIC)  

##  <a name="SSAS"></a> Analysis Services  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|可伸缩共享数据库|是||||||是|  
|备份/还原和附加/分离数据库|是|是|||||是|  
|同步数据库|是||||||是|  
|AlwaysOn 故障转移群集实例|是<br /><br /> 节点数是操作系统支持的最大值|是<br /><br /> 支持 2 个节点|||||是<br /><br /> 节点数是操作系统支持的最大值|  
|可编程性（AMO、ADOMD.Net、OLEDB、XML/A、ASSL、TMSL）|是|是|||||是|  
  
##  <a name="BIMD"></a> BI 语义模型（多维）  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|半累加性度量值|是|No <sup>1</sup>|||||是|  
|层次结构|是|是|||||是|  
|KPI|是|是|||||是|  
|透视|是||||||是|  
|操作|是|是|||||是|  
|帐户智能|是|是|||||是|  
|时间智能|是|是|||||是|  
|自定义汇总|是|是|||||是|  
|写回多维数据集|是|是|||||是|  
|写回维度|是||||||是|  
|写回单元|是|是|||||是|  
|钻取|是|是|||||是|  
|高级层次结构类型（父子、不规则层次结构）|是|是|||||是|  
|高级维度（引用维度、多对多维度）|是|是|||||是|  
|链接度量值和维度|是|是  <sup>2</sup> |||||是|  
|翻译|是|是|||||是|  
|Aggregations|是|是|||||是|  
|多个分区|是|支持，最多 3 个|||||是|  
|主动缓存|是||||||是|  
|自定义程序集（存储过程）|是|是|||||是|  
|MDX 查询和脚本|是|是|||||是|  
|DAX 查询|是|是|||||是|  
|基于角色的安全模型|是|是|||||是|  
|维度和单元级别的安全性|是|是|||||是|  
|可扩展字符串存储|是|是|||||是|  
|MOLAP、ROLAP 和 HOLAP 存储模式|是|是|||||是|  
|二进制和压缩的 XML 传输|是|是|||||是|  
|推送模式处理|是||||||是|  
|直接写回|是||||||是|  
|度量值表达式|是||||||是|  
  
 <sup>1</sup> Standard Edition 支持 LastChild 半累加性度量值，但不支持其他半累加性度量值，例如 None、FirstChild、FirstNonEmpty、LastNonEmpty、AverageOfChildren 和 ByAccount。 在所有版本上都支持累加性度量值（如 Sum、Count、Min 和 Max）和非累加性度量值 (DistinctCount)。  
  <sup>2</sup> Standard Edition 支持链接度量值和维度处于相同数据库，但不支持来自其他数据库或实例。
   
##  <a name="BIT"></a> BI 语义模型（表格）  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|层次结构|是|是|||||是|  
|KPI|是|是|||||是|  
|透视|是||||||是|  
|翻译|是|是|||||是|  
|DAX 计算、DAX 查询、MDX 查询|是|是|||||是|  
|行级安全性|是|是|||||是|  
|多个分区|是||||||是|  
|内存中存储模式|是|是|||||是|  
|DirectQuery 存储模式|是||||||是|  
  
##  <a name="PPSP"></a> Power Pivot for SharePoint  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|基于共享服务体系结构的 SharePoint 场集成|是||||||是|  
|用量报告|是||||||是|  
|运行状况监视规则|是||||||是|  
|PowerPivot 库|是||||||是|  
|PowerPivot 数据刷新|是||||||是|  
|PowerPivot 数据馈送|是||||||是|  
  
##  <a name="DM"></a> 数据挖掘  
  
|功能名称|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|标准算法|是|是|||||是|  
|数据挖掘工具（向导、编辑器、查询生成器）|是|是|||||是|  
|交叉验证|是||||||是|  
|挖掘结构数据的筛选子集的模型|是||||||是|  
|时序：ARTXP 和 ARIMA 方法之间的自定义混和|是||||||是|  
|时序：使用新数据的预测|是||||||是|  
|无限制并发数据挖掘查询|是||||||是|  
|数据挖掘算法的高级配置和优化选项|是||||||是|  
|支持插件算法|是||||||是|  
|并行模型处理|是||||||是|  
|时序：跨序列预测|是||||||是|  
|关联规则的无限制属性|是||||||是|  
|序列预测|是||||||是|  
|Naïve Bayes、神经网络和逻辑回归的多个预测目标|是||||||是|  
  
##  <a name="BIC"></a> Business Intelligence 客户端  
 以下软件客户端应用程序在 Microsoft 下载中心提供，它们旨在帮助你创建在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例上运行的商业智能文档。 当你在某一服务器环境中托管这些文档时，请使用支持该文档类型的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本。 下表标识哪一 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本包含承载在这些客户端应用程序中创建的文档所需的服务器功能。  
  
|工具名称|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|---------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|用于 Excel 和 Visio 2010 的数据挖掘外接程序（.xlsx、.vsdx）|是|是|||||是|  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 2010 和 2013 (.xlsx)|是||||||是|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] (.xlsx)|是||||||是|  
  
> [!NOTE]  
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 是一个使用数据模型创建工作簿的 Excel 加载项。  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] 不依赖于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]，但在 Excel 工作簿上使用 SharePoint 中的数据模型进行共享和协作时，需要 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]。 此功能是可作为 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise Edition 的一部分。  
>   
>      在 Excel 2016 中，Power Pivot 功能是内置的，因此不再需要 Power Pivot 加载项。  
> 2.  上表标识了启用这些客户端工具所需的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本；但是，这些工具可以访问在任何版本的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 上托管的数据。  
  
 ## 另请参阅  
 [SQL Server 2016 各个版本支持的功能](Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
 [SQL Server 2016 的产品规格](../Topic/Product%20Specifications%20for%20SQL%20Server%202016.md)   
 [安装 SQL Server 2016](../database-engine/install-windows/installation-for-sql-server-2016.md)  

