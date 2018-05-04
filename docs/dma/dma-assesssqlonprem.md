---
title: 执行 SQL Server 迁移评估 （数据迁移助手） |Microsoft 文档
ms.custom: ''
ms.date: 10/04/2017
ms.prod: sql
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: 42cd32f57547f811fba379caa3bef5678dc2b50b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="perform-a-sql-server-migration-assessment"></a>执行 SQL Server 迁移评估
下面的分步说明将帮助你迁移到本地 SQL Server，SQL Server 上的 Azure VM 或 Azure SQL 数据库，运行通过使用数据迁移助手执行你的第一个评估。

## <a name="create-an-assessment"></a>创建评估

1.  选择**新建**（+） 图标，，然后选择**评估**项目类型。

2.  设置源和目标服务器类型。

    如果您正在升级你的本地 SQL Server 实例到现代的在本地 SQL Server 实例或托管在 Azure VM 上的 SQL Server，将源和目标服务器类型设置为**SQL Server**。 如果你要迁移到 Azure SQL 数据库，而是将目标服务器类型设置为**Azure SQL 数据库**。

3.  单击 **“创建”**。

    ![创建评估](../dma/media/NewAssessment.png)

## <a name="choose-assessment-options"></a>选择评估选项

1. 选择你打算迁移到目标 SQL Server 版本。

2. 选择报表类型。

   在正在评估源 SQL Server 实例迁移到本地 SQL Server 或托管在 Azure VM 目标上的 SQL Server，你可以选择一个或两个以下的评估报表类型：

    -   **兼容性问题**

    -   **新功能的建议**

    ![选择 SQL Server 目标评估报表类型](../dma/media/AssessmentTypes.png)

   在正在评估源 SQL Server 实例迁移到 Azure SQL 数据库，你可以选择一个或两个以下的评估报表类型：

    -   **检查数据库兼容性**

    -   **检查功能奇偶校验**

    ![选择 SQL 数据库目标的评估报表类型](../dma/media/AssessmentTypes_Azure.png)

## <a name="add-databases-to-assess"></a>添加要评估的数据库

1.  选择**添加源**以打开连接弹出菜单。

2.  输入 SQL server 实例名称，选择身份验证类型、 设置正确的连接属性，然后选择**连接**。

3.  选择数据库以评估，然后选择**添加**。

    > [!NOTE] 
    > 你可以通过选择它们时按住 Shift 或 Ctrl 键，，然后单击移除多个数据库**删除源**。 你还可以添加数据库来自多个 SQL Server 实例使用**添加源**按钮。

4.  单击**下一步**启动评估。

    ![添加源和启动评估](../dma/media/SelectDatabase.png)

## <a name="view-results"></a>查看结果

评估的持续时间取决于添加的数据库数和每个数据库的架构大小。 一旦可用，将为每个数据库中显示结果。

1.  选择已完成评估，该数据库，然后切换**兼容性问题**和**功能建议**通过使用切换器。

2.  跨所有兼容性级别的目标 SQL Server 版本支持你在上选择查看兼容性问题**选项**页。

你可以通过分析受影响的对象，其下发现每个问题的详细信息中查看兼容性问题**重大更改**，**行为更改**，和**已弃用的功能**.

![查看评估结果](../dma/media/ReviewResults.png)

同样，你可以查看功能建议跨**性能**，**存储**，和**安全**区域。

功能建议涵盖大量的内存中 OLTP 和列存储、 Stretch Database，始终加密，动态数据屏蔽和透明数据加密等功能。

![视图功能建议](../dma/media/FeatureRecommendations.png)

对于 Azure SQL 数据库，评估提供迁移阻塞问题和功能奇偶校验问题。 通过选择特定的选项来查看这两个类别的结果。

- **SQL Server 功能奇偶校验**类别提供了全面的建议，在 Azure 中和缓解措施中可用的其他方法。 它可帮助你规划迁移项目中的此工作量。

  ![查看 SQL Server 功能奇偶校验的信息](../dma/media/SQLFeatureParity.png)

- **兼容性问题**类别提供部分支持或不受支持的功能，能够阻止将本地 SQL Server 数据库迁移到 Azure SQL 数据库。 然后，它提供了建议，以帮助您解决这些问题。

  ![视图兼容性问题](../dma/media/CompatibilityIssues.png)

## <a name="export-results"></a>导出结果

所有数据库都完成评估后，选择**导出报表**将结果导出到 JSON 文件或 CSV 文件中。 然后，你可以在自己方便时分析数据。

你可以同时运行多个评估并通过打开查看的评估状态**所有评估**页。
