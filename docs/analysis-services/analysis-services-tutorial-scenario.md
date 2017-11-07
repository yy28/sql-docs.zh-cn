---
title: "Analysis Services 教程的情况下 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 2f5b1a42-b814-4d7d-b603-5383d9ac66b9
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 933a07504d0237d67becb2d98e1f5271548cb14a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="analysis-services-tutorial-scenario"></a>Analysis Services 教程方案
本教程基于 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)]，这是一家虚构的公司。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 是一家大型跨国制造公司，生产金属复合材料的自行车，产品远销北美、欧洲和亚洲市场。 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 公司总部设在华盛顿州的伯瑟尔市，雇佣了 500 名工人。 此外，在 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 市场中还活跃着一些地区销售团队。  
  
在最近几年中， [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 购买了位于墨西哥的小型生产厂 Importadores Neptuno。 Importadores Neptuno 为 [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 产品系列生产多种关键子组件。 这些子组件将被运送到伯瑟尔市进行最后的产品装配。 在 2005 年，Importadores Neptuno 转型成为专注于旅游登山车系列产品的独立制造商和销售商。  
  
实现一个成功的会计年度之后， [!INCLUDE[ssSampleDBCoFull](../includes/sssampledbcofull-md.md)] 现在希望通过以下方法扩大市场份额：专注于向高端客户提供产品、通过外部网站扩展其产品的销售渠道、通过降低生产成本来削减其销售成本。  
  
## <a name="current-analysis-environment"></a>当前分析环境  
为了支持销售和营销团队以及高级管理人员的数据分析需要，公司当前从 [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] 数据库中提取事务数据，从电子表格中提取诸如销售配额之类的非事务信息，并将这些信息合并到 **AdventureWorksDW2012** 关系数据仓库。 但是，关系数据仓库存在下列问题：  
  
-   报表是静态的。 用户无法通过交互方式探测报表中的数据以获取更详细的信息，例如他们可以处理 [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 透视表。 虽然现有的一组预定义报表足以供许多用户使用，但更高级的用户却需要对数据库进行直接查询访问，以进行交互式查询和访问专用报表。 但是，由于 **AdventureWorksDW2012** 数据库非常复杂，因此，这类用户需要花费大量时间来掌握如何创建有效查询。  
  
-   查询性能差异很大。 例如，有些查询只需几秒钟便可非常迅速地返回结果，而另一些查询需要几分钟才能返回结果。  
  
-   聚合表难以管理。 在尝试缩短查询响应时间方面， [!INCLUDE[ssSampleDBCoShort](../includes/sssampledbcoshort-md.md)] 数据仓库团队已在 **AdventureWorksDW2012** 数据库中生成几种聚合表。 例如，他们生成了一种按月汇总销售额的表。 然而，尽管这些聚合表可显著提高查询性能，但是，他们所生成的用于在一段时间内维护这些表的基础结构却容易破坏并出现错误。  
  
-   复杂的计算逻辑隐藏在报表定义中，所以很难在报表之间共享。 由于这种业务逻辑针对每个报表单独生成，因此，各个报表的汇总信息有时是不同的。 所以，管理人员对数据仓库报表数据的信任度是有限的。  
  
-   用户所在的业务部门不同，其感兴趣的数据视图也不同。 每个组都很难理解与其不相关的数据元素。  
  
-   对于需要专用报表的用户而言，计算逻辑非常具有挑战性。 由于这类用户必须为每个报表单独定义计算逻辑，因此，无法对如何定义计算逻辑进行集中控制。 例如，有些用户知道他们应使用基本统计技术（如移动平均值），但他们却不知道如何构建此类计算，因而也就无从使用这些技术。  
  
-   组合相关的信息集时存在难度。 业务用户很难构造一些专用查询，以组合两个相关的信息集（如销售额和销售配额）。 此类查询会占用大量的数据库空间，因此，公司要求用户向数据仓库团队请求跨主题区域的数据集。 因此，仅定义了少数预定义报表，这些报表可以用于组合来自多个主题区域的数据。 此外，由于这些报表非常复杂，因此用户不愿尝试修改这些报表。  
  
-   报表主要提供美国的业务信息。 非美国分公司的用户非常不满意只提供美国的业务信息，他们希望能够查看不同货币和不同语言的报表。  
  
-   信息难以审核。 财务部门当前仅将 **AdventureWorksDW2012** 数据库用作从中进行大容量查询的数据源。 然后，再将数据下载到单个电子表格中，并花费大量时间准备数据和处理电子表格。 因此，很难在整个公司内准备、审核和管理公司财务报表。  
  
## <a name="the-solution"></a>解决方案  
数据仓库团队最近对当前分析系统执行了设计评审。 评审包括当前问题和未来需求之间的差距分析。 数据仓库团队已确定 **AdventureWorksDW2012** 数据库是一个设计良好的维度数据库，具有相符的维度和代理键。 相符的维度可使某个维度用于多个数据集市中，例如时间维度或产品维度。 代理键是链接维度表和事实数据表的假键，用于确保唯一性并提高性能。 此外，数据仓库团队已确定当前在加载和管理 **AdventureWorksDW2012** 数据库中的基表方面没有重大问题。 因此，该团队已决定使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 来完成下列各项：  
  
-   通过一个通用的元数据层提供统一的数据访问以进行分析和报告。  
  
-   简化用户的数据视图，从而加速交互式查询、预定义查询以及预定义报表的开发。  
  
-   正确构造可组合来自多个主题区域的数据的查询。  
  
-   管理聚合。  
  
-   存储和重用复杂的计算。  
  
-   为美国以外的业务用户提供本地化体验。  
  
Analysis Services 教程中的课程提供生成满足上述所有目标的多维数据集数据库的指南。 若要开始，请继续第一课： [第 1 课：创建新的表格模型项目](../analysis-services/lesson-1-create-a-new-tabular-model-project.md)。  
  
## <a name="see-also"></a>另请参阅  
[多维建模（Adventure Works 教程）](../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)  
  
  
  

