---
title: "SQL Server 各个版本支持的 Integration Services 功能 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
caps.latest.revision: 15
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# SQL Server 各个版本支持的 Integration Services 功能
 本主题提供有关不同版本的 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]所支持的 SQL Server Integration Services (SSIS) 功能的详细信息。  

有关评估版和开发人员版支持的功能，请参阅 SQL Server 企业版。 
  
有关最新的发布说明和新增功能的信息，请参阅以下内容：
-   [SQL Server 2016 发行说明](../sql-server/sql-server-2016-release-notes.md)
-   [SQL Server 2016 Integration Services 中的新增功能](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [SQL Server vNext Integration Services 中的新增功能](../integration-services/what-s-new-in-integration-services-in-sql-server-vnext.md)
    
**试用 SQL Server 2016！**    

可在 180 天的试用期内使用 SQL Server 评估版。  
    
> [![从评估中心下载](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[从评估中心下载 SQL Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Azure 虚拟机小](../analysis-services/media/azure-virtual-machine-small.png)**启动已安装 SQL Server 2016 的虚拟机[](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)**    

##  <a name="a-nameisanew-integration-services-features-in-sql-server-vnext"></a><a name="IS"></a>SQL Server vNext 中的新 Integration Services 功能
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|扩展|是||||||是|
|支持 OData 组件 <sup>1</sup> 中的 Microsoft Dynamics AX 和 Microsoft Dynamics CRM|是|用户帐户控制|||||是|

<sup>1</sup>SQL Server 2016 Service Pack 1 中也支持此功能。

##  <a name="a-nameisa-integration-services"></a><a name="IS"></a> Integration Services  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|内置数据源连接器|是|用户帐户控制|用户帐户控制|用户帐户控制|用户帐户控制|用户帐户控制|是|  
|Azure 数据源连接器和任务|是|用户帐户控制|用户帐户控制|用户帐户控制|用户帐户控制|用户帐户控制|是|  
|SQL Server 导入和导出向导|是|用户帐户控制|用户帐户控制|用户帐户控制|用户帐户控制|用户帐户控制|是|  
|Hadoop / HDFS 连接器和任务|是|用户帐户控制|用户帐户控制||||是|  
|SSIS 设计器和运行时|是|用户帐户控制|||||是|  
|内置任务和转换|是|用户帐户控制|||||是|  
|基本数据探查工具|是|用户帐户控制|||||是|  
|Change Data Capture Service for Oracle by Attunity|是||||||是|  
|Change Data Capture Designer for Oracle by Attunity|是||||||是| 

##  <a name="a-nameisaaa-integration-services---advanced-adapters"></a><a name="ISAA"></a> Integration Services - 高级适配器  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|高性能 Oracle 目标|是||||||是|  
|高性能 Teradata 目标|是||||||是|  
|SAP BW 源和目标|是||||||是|  
|数据挖掘模型定型目标适配器|是||||||是|  
|维度处理目标适配器|是||||||是|  
|分区处理目标适配器|是||||||是|  
|Attunity 提供的变更数据捕获组件|是||||||是|  
|Attunity 提供的开放式数据库连接 (ODBC)|是||||||是|  
  
##  <a name="a-nameisata-integration-services---advanced-transforms"></a><a name="ISAT"></a> Integration Services - 高级转换  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|持续性（高性能）查找|是||||||是|  
|数据挖掘查询转换|是||||||是|  
|模糊分组和查找转换|是||||||是|  
|术语提取和查找转换|是||||||是|  
  