---
title: Analysis Services 的 SQL Server 2016 各个版本支持的功能 |Microsoft 文档
ms.custom: ''
ms.date: 06/29/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: multidimensional-tabular
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f09d7be1-bd63-43f8-b91c-bf19166b4457
caps.latest.revision: 4
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e79ca3b24ec8ef92f677044795ede8303a3b4062
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="analysis-services-features-supported-by-sql-server-editions"></a>支持的 SQL Server 版本的 analysis Services 功能
[!INCLUDE[ssas-appliesto-sql2016-later](../includes/ssas-appliesto-sql2016-later.md)]

本主题提供支持的不同版本的 SQL Server 2016 Analysis Services 功能的详细的信息。 Evaluation 和 Developer 版本支持的功能，请参阅 Enterprise edition。

## <a name="analysis-services-servers"></a>Analysis Services （服务器）
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|可伸缩共享数据库|是||||||是|  
|备份/还原和附加/分离数据库|是|用户帐户控制|||||是|  
|同步数据库|是||||||是|  
|AlwaysOn 故障转移群集实例|是<br /><br /> 节点数是操作系统支持的最大值|是<br /><br /> 支持 2 个节点|||||是<br /><br /> 节点数是操作系统支持的最大值|  
|可编程性（AMO、ADOMD.Net、OLEDB、XML/A、ASSL、TMSL）|是|用户帐户控制|||||是|  
  
## <a name="tabular-models"></a>表格模型 
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|层次结构|是|用户帐户控制|||||是|  
|KPI|是|用户帐户控制|||||是|  
|透视|是||||||是|  
|翻译|是|用户帐户控制|||||是|  
|DAX 计算、DAX 查询、MDX 查询|是|用户帐户控制|||||是|  
|行级安全性|是|用户帐户控制|||||是|  
|多个分区|是||||||是|  
|内存中存储模式|是|用户帐户控制|||||是|  
|DirectQuery 存储模式|是||||||是|  

## <a name="multidimensional-models"></a>多维模型 
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|半累加性度量值|是|No <sup>1</sup>|||||是|  
|层次结构|是|用户帐户控制|||||是|  
|KPI|是|用户帐户控制|||||是|  
|透视|是||||||是|  
|操作|是|用户帐户控制|||||是|  
|帐户智能|是|用户帐户控制|||||是|  
|时间智能|是|用户帐户控制|||||是|  
|自定义汇总|是|用户帐户控制|||||是|  
|写回多维数据集|是|用户帐户控制|||||是|  
|写回维度|是||||||是|  
|写回单元|是|用户帐户控制|||||是|  
|钻取|是|用户帐户控制|||||是|  
|高级层次结构类型（父子、不规则层次结构）|是|用户帐户控制|||||是|  
|高级维度（引用维度、多对多维度）|是|用户帐户控制|||||是|  
|链接度量值和维度|是|是  <sup>2</sup> |||||是|  
|翻译|是|用户帐户控制|||||是|  
|Aggregations|是|用户帐户控制|||||是|  
|多个分区|是|支持，最多 3 个|||||是|  
|主动缓存|是||||||是|  
|自定义程序集（存储过程）|是|用户帐户控制|||||是|  
|MDX 查询和脚本|是|用户帐户控制|||||是|  
|DAX 查询|是|用户帐户控制|||||是|  
|基于角色的安全模型|是|用户帐户控制|||||是|  
|维度和单元级别的安全性|是|用户帐户控制|||||是|  
|可扩展字符串存储|是|用户帐户控制|||||是|  
|MOLAP、ROLAP 和 HOLAP 存储模式|是|用户帐户控制|||||是|  
|二进制和压缩的 XML 传输|是|用户帐户控制|||||是|  
|推送模式处理|是||||||是|  
|直接写回|是||||||是|  
|度量值表达式|是||||||是|  
  
 <sup>1</sup> Standard Edition 支持 LastChild 半累加性度量值，但不支持其他半累加性度量值，例如 None、FirstChild、FirstNonEmpty、LastNonEmpty、AverageOfChildren 和 ByAccount。 在所有版本上都支持累加性度量值（如 Sum、Count、Min 和 Max）和非累加性度量值 (DistinctCount)。  
  <sup>2</sup> standard edition 支持链接度量值和维度内的同一数据库中，而不是从其他数据库或实例。
  
## <a name="power-pivot-for-sharepoint"></a>Power Pivot for SharePoint  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|基于共享服务体系结构的 SharePoint 场集成|是||||||是|  
|用量报告|是||||||是|  
|运行状况监视规则|是||||||是|  
|PowerPivot 库|是||||||是|  
|PowerPivot 数据刷新|是||||||是|  
|PowerPivot 数据馈送|是||||||是|  
  
## <a name="data-mining"></a>数据挖掘  
  
|功能名称|Enterprise|Standard|Web|Express with Advanced Services|Express with Tools|Express|开发人员|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|-------------|---------------|  
|标准算法|是|用户帐户控制|||||是|  
|数据挖掘工具（向导、编辑器、查询生成器）|是|用户帐户控制|||||是|  
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
  
 ## <a name="see-also"></a>另请参阅  
 [SQL Server 2016 的产品规格](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)   
 [安装 SQL Server](../database-engine/install-windows/installation-for-sql-server-2016.md)  


