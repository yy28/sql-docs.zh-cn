---
title: "Analysis Services 中的表格模型的兼容性级别 |Microsoft 文档"
ms.custom: 
ms.date: 10/16/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.bidtoolset.versioncompat.f1
ms.assetid: 8943d78d-4a73-4be8-ad14-3d428f5abd06
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: d194cdfa2771b96f2ae1880f474b8a0107e0b67c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Analysis Services 表格模型的兼容性级别
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  *兼容性级别*指的是特定于版本的 Analysis Services 引擎中的行为。 例如，DirectQuery 和表格对象元数据根据兼容性级别具有不同的实现。 在常规应选择你的服务器支持的最新兼容性级别。

  **最新的兼容性级别为 1400** 
  
1400 兼容级别中的主要功能包括：

*  新的基础结构的数据连接和导入表格模型支持 TOM Api 和 TMSL 脚本。 这使对其他数据源，例如 Azure Blob 存储的支持。 其他数据源将包含在后续更新。
*  数据转换，并通过使用获取数据和 M 表达式的数据混合应用程序功能。
*  度量值现在支持具有 DAX 表达式中，启用 BI 工具 （如 Microsoft Excel) 深化到详细数据从聚合报表的详细信息行属性。 例如，当最终用户查看地区和月的总销售额，则可查看关联的订单详细信息。 
*  表名和列名，除了在其中的数据的对象级别安全。
*  不规则层次结构的增强的支持。
*  性能和监视改进。

  
## <a name="supported-compatibility-levels-by-version"></a>版本支持的兼容级别
  
|||  
|-|-|- 
|**兼容级别**|**服务器版本**| 
|1400|Azure Analysis Services，SQL Server 自 2017 年 1 |  
|1200|Azure Analysis Services，SQL Server 自 2017 年，SQL Server 2016| 
|1103|SQL Server 自 2017 年 1 *，SQL Server 2016、 SQL Server 2014、 SQL Server 2012 SP1|  
|1100|SQL Server 自 2017 年 1 *，SQL Server 2016、 SQL Server 2014、 SQL Server 2012 SP1、 SQL Server 2012| 

\*在 SQL Server 自 2017 年，1100年和 1103年兼容性级别已弃用。
  
## <a name="set-compatibility-level"></a>将兼容性级别设置 
 如果创建新的表格模型项目之后在 SQL Server Data Tools (SSDT)，你可以在指定的兼容性级别**表格模型设计器**对话框。 
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.png)  
  
 如果你选择**不要再显示此消息**选项，所有后续项目都将使用默认值为指定的兼容性级别。 你可以更改在 SSDT 中的默认兼容级别**工具** > **选项**。  
  
 若要升级在 SSDT 的表格模型项目，将设置**兼容性级别**模型中的属性**属性**窗口。 请记住，升级兼容性级别是不可逆。
  
## <a name="check-compatibility-level-for-a-database-in-ssms"></a>检查 SSMS 中数据库的兼容级别  
 在 SSMS 中，右键单击数据库名称 >**属性** > **兼容性级别**。  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>检查 SSMS 中支持的服务器兼容级别  
 在 SSMS 中，右键单击服务器名称 >**属性** > **支持兼容性级别**。  
  
 此属性指定的数据库将在服务器运行的最高的兼容性级别。 支持的兼容级别为只读，无法更改。  
  
## <a name="see-also"></a>另请参阅  
 [多维数据库的兼容级别](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [什么是 Analysis Services 中的新增功能](../../analysis-services/what-s-new-in-analysis-services.md)   
 [创建新的表格模型项目](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  
