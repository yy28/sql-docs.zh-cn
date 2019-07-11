---
title: SQL Server 各个版本支持的 analysis Services 功能 |Microsoft Docs
ms.date: 07/10/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6d4f0cc16638963dbbbb091bc19cade36e45fe3b
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792553"
---
# <a name="analysis-services-features-supported-by-sql-server-edition"></a>支持的 SQL Server 版本的 analysis Services 功能

[!INCLUDE[ssas-appliesto-sql2016-later](../includes/ssas-appliesto-sql2016-later.md)]

本文介绍了不同版本的 SQL Server 2016、 2017，2019 Analysis Services 支持的功能。 评估版支持企业版功能。

## <a name="analysis-services-servers"></a>Analysis Services （服务器）
  
|功能|Enterprise|标准|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|可伸缩共享数据库|是||||||是|  
|备份/还原和附加/分离数据库|是|是|||||是|  
|同步数据库|是||||||是|  
|AlwaysOn 故障转移群集实例|是<br /><br /> 节点数是操作系统支持的最大值|是<br /><br /> 支持 2 个节点|||||是<br /><br /> 节点数是操作系统支持的最大值|  
|可编程性（AMO、ADOMD.Net、OLEDB、XML/A、ASSL、TMSL）|是|是|||||是|  
  
## <a name="tabular-models"></a>表格模型 
  
|功能|Enterprise|标准|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|层次结构|是|是|||||是|  
|KPI|是|是|||||是|  
|透视|是||||||是|  
|翻译|是|是|||||是|  
|DAX 计算、DAX 查询、MDX 查询|是|是|||||是|  
|行级安全性|是|是|||||是|  
|多个分区|是||||||是|  
|计算组|是 （从 SQL Server 2019 开始）|是 （从 SQL Server 2019 开始）|||||是 （从 SQL Server 2019 开始）|  
|内存中存储模式|是|是|||||是|  
|DirectQuery 模式|是|是 （从 SQL Server 2019 开始）|||||是|  

## <a name="multidimensional-models"></a>多维模型 
  
|功能|Enterprise|标准|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|半累加性度量值|是|否<sup> [1](#sameas)</sup>|||||是|  
|层次结构|是|是|||||是|  
|KPI|是|是|||||是|  
|透视|是||||||是|  
|操作|是|是|||||是|  
|帐户智能|是|是|||||是|  
|时间智能|是|是|||||是|  
|自定义汇总|是|是|||||是|  
|写回多维数据集|是|是|||||是|  
|写回维度|是 <sup>[2](#wb)</sup>||||||是 <sup>[2](#wb)</sup>|  
|写回单元|是|是|||||是|  
|钻取|是|是|||||是|  
|高级层次结构类型（父子、不规则层次结构）|是|是|||||是|  
|高级维度（引用维度、多对多维度）|是|是|||||是|  
|链接度量值和维度|是|是<sup> [3](#linkmd)</sup> |||||是|  
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
|度量值表达式|是||||||是|  
  
<a name="sameas">[1]</a> Standard edition 支持 LastChild 半累加性度量值，但其他半累加性度量值，例如 None、 FirstChild、 FirstNonEmpty、 LastNonEmpty、 AverageOfChildren 和 ByAccount。 在所有版本上都支持累加性度量值（如 Sum、Count、Min 和 Max）和非累加性度量值 (DistinctCount)。 

<a name="wb">[2]</a>写回维度已不再使用 SQL Server Analysis Services 2019 及更高版本。
 
<a name="linkmd">[3]</a> Standard edition 支持链接度量值和维度处于相同的数据库，但不能从其他数据库或实例。
  
  
## <a name="power-pivot-for-sharepoint"></a>Power Pivot for SharePoint  
  
|功能|Enterprise|标准|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|基于共享服务体系结构的 SharePoint 场集成|是||||||是|  
|用量报告|是||||||是|  
|运行状况监视规则|是||||||是|  
|PowerPivot 库|是||||||是|  
|PowerPivot 数据刷新|是||||||是|  
|PowerPivot 数据馈送|是||||||是|  
  
## <a name="data-mining"></a>数据挖掘  

> [!NOTE]
> 数据挖掘是[弃用](analysis-services-backward-compatibility-sql2017.md#deprecated-features)SQL Server Analysis Services 2017 中。
  
|功能名称|Enterprise|标准|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|标准算法|是|是|||||是|  
|数据挖掘工具（向导、编辑器、查询生成器）|是|是|||||是|  
|交叉验证|是||||||是|  
|挖掘结构数据的筛选子集的模型|是||||||是|  
|时序：自定义混和 ARTXP 和 ARIMA 方法之间|是||||||是|  
|时序：使用新数据的预测|是||||||是|  
|无限制并发数据挖掘查询|是||||||是|  
|数据挖掘算法的高级配置和优化选项|是||||||是|  
|支持插件算法|是||||||是|  
|并行模型处理|是||||||是|  
|时序：跨序列预测|是||||||是|  
|关联规则的无限制属性|是||||||是|  
|序列预测|是||||||是|  
|Naïve Bayes、神经网络和逻辑回归的多个预测目标|是||||||是|  
  


