---
title: "Integration Services 的 SQL Server 版本支持的功能 |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e5018225-68bb-4f34-ae4a-ead79d8ad13a
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 8cc1fcfdeae8742a93916dfb08c9db1215f88721
ms.openlocfilehash: e9d1b8851f113fa44264230a79d0e496007ed96b
ms.contentlocale: zh-cn
ms.lasthandoff: 10/17/2017

---
# <a name="integration-services-features-supported-by-the-editions-of-sql-server"></a>Integration Services 功能的 SQL Server 各个版本支持
 本主题提供有关不同版本的 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]所支持的 SQL Server Integration Services (SSIS) 功能的详细信息。  

Evaluation 和 Developer 版本支持的功能，请参阅下表中列出的企业版功能。
  
有关最新的发行说明和新的信息是什么，请参阅以下文章：
-   [SQL Server 2016 发行说明](../sql-server/sql-server-2016-release-notes.md)
-   [SQL Server 2016 Integration Services 中的新增功能](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)
-   [SQL Server 2017 Integration Services 中的新增功能](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)
    
**试用 SQL Server 2016！**    

可在 180 天的试用期内使用 SQL Server 评估版。  
    
> [![从评估中心下载](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[从评估中心下载 SQL Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
## <a name="ISNew"></a>新的 Integration Services 功能的 SQL Server 自 2017 年
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|横向扩展 Master|是|||||
|横向扩展辅助进程|是|是 <sup>1</sup>|TBD|TBD|TBD|
|对 Microsoft Dynamics AX 和 Microsoft Dynamics CRM OData 组件中的支持<sup>2</sup>|是|是||||

<sup>1</sup>运行包，需要在向外扩展的仅限企业的功能，如果员工出缩放还必须在 SQL Server Enterprise 的实例上运行。

<sup>2</sup> Service Pack 1 的 SQL Server 2016 也支持此功能。

## <a name="IEWiz"></a>SQL Server 导入和导出向导

|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL Server 导入和导出向导|是|是|是|是|是|  

## <a name="IS"></a> Integration Services  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|内置数据源连接器|是|是|||| 
|内置任务和转换|是|是||||  
|ODBC 源和 by Attunity 的目标|是|是|||| 
|Azure 数据源连接器和任务|是|是||||  
|Hadoop/HDFS 连接器和任务|是|是||||  
|基本数据探查工具|是|是|||| 

## <a name="ISAA"></a>Integration Services-高级源和目标  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|高性能 Oracle 源和 by Attunity 的目标|是|||||  
|高性能 Teradata 源和 by Attunity 的目标|是|||||  
|SAP BW 源和目标|是|||||  
|数据挖掘模型定型目标|是|||||  
|维度处理目标|是|||||  
|分区处理目标|是|||||  
  
## <a name="ISAT"></a>Integration Services-高级任务和转换  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|变更数据捕获组件 by Attunity <sup>1</sup>|是|||||  
|数据挖掘查询转换|是|||||  
|模糊分组和模糊查找转换|是|||||  
|字词提取和字词查找转换|是|||||  

<sup>1</sup> by Attunity 的变更数据捕获组件需要 Enterprise edition。 Change Data Capture Service 和 Change Data Capture Designer，但是，不需要 Enterprise edition。 你可以使用设计器和服务的计算机上未安装 SSIS 其中。

