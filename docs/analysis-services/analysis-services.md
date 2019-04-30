---
title: 了解 SQL Server Analysis Services |Microsoft Docs
ms.date: 12/05/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: overview
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b2cd892ad41beba2b5715b3a7186ae5e44bb7911
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63206354"
---
# <a name="about-sql-server-analysis-services"></a>关于 SQL Server Analysis Services

Analysis Services 是在决策支持和商业分析中使用的分析数据引擎。 它提供了企业级语义数据模型为商业报表和客户端应用程序，如 Power BI、 Excel、 Reporting Services 报表和其他数据可视化工具。

典型的工作流包括在 Visual Studio 中创建的表格或多维数据模型项目、 将模型部署为服务器实例的数据库、 设置重复执行的数据处理和分配权限以允许最终用户通过数据访问。 准备就绪时，支持 Analysis Services 作为数据源的客户端应用程序可以访问你语义数据模型。

Analysis Services 现已推出两个不同的平台：

**Azure Analysis Services** -支持 1200年及更高版本的兼容性级别的表格模型。 可支持 DirectQuery、分区、行级安全性、双向关系和翻译。 若要了解详细信息，请参阅[Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/)。

**SQL Server Analysis Services** -支持表格模型在所有兼容性级别、 多维模型、 数据挖掘和 Powerpivot for SharePoint。

## <a name="documentation-by-area"></a>文档（按区域）

一般情况下， [Azure Analysis Services 文档](https://docs.microsoft.com/azure/analysis-services/)附带 Azure 文档。 如果有兴趣在云中具有表格模型，最好从这里开始。 此文章和在本部分中的文档是主要用于 SQL Server Analysis Services。 但是，至少对于表格模型中，如何创建和部署表格模型项目是大致相同，而不考虑您所使用的平台。 请查看以下各节，了解详细信息：

- [比较表格和多维解决方案](../analysis-services/comparing-tabular-and-multidimensional-solutions-ssas.md)
- [安装 SQL Server Analysis Services](../analysis-services/instances/install-windows/install-analysis-services.md)
- [表格模型](../analysis-services/tabular-models/tabular-models-ssas.md)
- [多维模型](../analysis-services/multidimensional-models/multidimensional-models-ssas.md)
- [数据挖掘](../analysis-services/data-mining/data-mining-ssas.md)
- [Power Pivot for SharePoint](../analysis-services/power-pivot-sharepoint/power-pivot-for-sharepoint-ssas.md)
- [教程](../analysis-services/analysis-services-tutorials-ssas.md)
- [服务器管理](../analysis-services/instances/analysis-services-instance-management.md)
- [开发人员文档](analysis-services-developer-documentation.md)
- [技术参考](https://docs.microsoft.com/bi-reference/)

#### <a name="see-also"></a>请参阅

[Azure Analysis Services 文档](https://docs.microsoft.com/azure/analysis-services/)
[SQL Server 文档](../sql-server/sql-server-technical-documentation.md)
