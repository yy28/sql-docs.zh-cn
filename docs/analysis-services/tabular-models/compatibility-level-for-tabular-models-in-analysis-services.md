---
title: 在 Analysis Services 中表格模型的兼容级别 |Microsoft Docs
ms.date: 06/10/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 19c69aa1a1ab27e7498d3c9d6a0d52c25b9f0020
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66826828"
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a>Analysis Services 表格模型的兼容性级别
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  *兼容性级别*指的是功能和功能增强功能，同时将 Analysis Services 引擎和表格模型元数据。 在常规应选择你的服务器支持的最新兼容性级别。 

  **最新的受支持的兼容性级别是 1400** 
  
在 1400年兼容级别中的主要功能包括：

*  新的基础结构的数据连接和导入表格模型支持 TOM Api 和 TMSL 脚本。 这使对 Azure Blob 存储等其他数据源的支持。 其他数据源将包含在后续更新。
*  数据转换，并通过使用 SQL Server Data Tools (SSDT) 中的获取数据和 M 表达式的数据混合功能。
*  度量值现在支持使用启用 BI 的 DAX 表达式的详细信息行属性工具如 Microsoft Excel 向下钻取到详细聚合报表中的数据。 例如，当用户查看某个区域和月份的销售总额，他们可以查看关联的订单详细信息。 
*  表和列名称，以及其中的数据的对象级安全性。
*  不规则层次结构的增强的支持。
*  性能和监视改进。

  
## <a name="supported-compatibility-levels-by-version"></a>版本支持的兼容级别
  
较低的兼容性级别支持向后兼容性。 

|||  
|-|-|- 
|**兼容级别**|**服务器版本**| 
|1470|SQL Server 2019 (CTP 2.3 和更高版本) | 
|1400|Azure Analysis Services, SQL Server 2019, SQL Server 2017 |  
|1200|Azure Analysis Services, SQL Server 2019, SQL Server 2017, SQL Server 2016| 
|1103|SQL Server 2017*, SQL Server 2016, SQL Server 2014, SQL Server 2012 SP1|  
|1100|SQL Server 2017 *，SQL Server 2016、 SQL Server 2014、 SQL Server 2012 SP1、 SQL Server 2012| 

\* 在 SQL Server 2017 及更高版本，不推荐使用 1100年和 1103年兼容级别。
  
## <a name="set-compatibility-level"></a>设置兼容级别 
 在创建新的表格模型项目时在 SQL Server Data Tools (SSDT)，可以指定兼容性级别上**表格模型设计器**对话框。 
  
 ![ssas_tabularproject_compat1200](../../analysis-services/tabular-models/media/ssas-tabularproject-compat1200.png)  
  
 如果选择**不再显示此消息**选项，所有后续项目将使用默认值为指定的兼容性级别。 你可以在 SSDT 中的默认兼容级别**工具** > **选项**。  
  
 若要升级在 SSDT 中的表格模型项目，请设置**兼容性级别**模型中的属性**属性**窗口。 请记住，升级兼容性级别是不可逆。
  
## <a name="check-compatibility-level-for-a-database-in-ssms"></a>检查 SSMS 中数据库的兼容级别  
 在 SSMS 中，右键单击数据库名称 >**属性** > **兼容性级别**。  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a>检查 SSMS 中支持的服务器兼容级别  
 在 SSMS 中，右键单击服务器名称 >**属性** > **支持的兼容级别**。  

 此属性指定的数据库，将在服务器上运行的最高的兼容性级别。 支持的兼容级别为只读，无法更改。
 
> [!NOTE]  
>  在 SSMS 中，当连接到 SQL Server Analysis Services 服务器、 Azure Analysis Services 服务器或 Power BI Premium 工作区中，支持的兼容级别属性将显示 1200年。 这是一个已知的问题，会在即将发布的 SSMS 中解决更新。 解析时，此属性将显示最高支持的兼容级别。 
  
## <a name="see-also"></a>请参阅  
 [多维数据库的兼容性级别](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [What's new in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [创建新的表格模型项目](../../analysis-services/tabular-models/create-a-new-tabular-model-project-analysis-services.md)  
  
  
