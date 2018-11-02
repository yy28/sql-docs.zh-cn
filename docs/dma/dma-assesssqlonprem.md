---
title: 执行 SQL Server 迁移评估 （数据迁移助手） |Microsoft Docs
description: 了解如何使用数据迁移助手迁移到另一个 SQL Server 或 Azure SQL 数据库之前，评估的本地 SQL Server
ms.custom: ''
ms.date: 10/20/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: pochiraju
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 12c91f52694c9c7b4cc9abc9e7b96df0ddffb51c
ms.sourcegitcommit: f9b4078dfa3704fc672e631d4830abbb18b26c85
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2018
ms.locfileid: "50965947"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>执行使用数据迁移助手的 SQL Server 迁移评估

以下分步说明帮助你迁移到本地 SQL Server，使用数据迁移助手的 Azure VM 或 Azure SQL 数据库上运行的 SQL Server 执行第一个评估。

## <a name="create-an-assessment"></a>创建评估

1.  选择**新建**（+） 图标，并选择**评估**项目类型。

2.  设置源和目标服务器类型。

    如果您要升级的本地 SQL Server 实例到最新的本地 SQL Server 实例或 Azure VM 上托管的 SQL Server，源和目标服务器类型设置为**SQL Server**。 如果要迁移到 Azure SQL 数据库，而是将目标服务器类型设置为**Azure SQL 数据库**。

3.  单击 **“创建”**。

    ![创建评估](../dma/media/NewAssessment.png)

## <a name="choose-assessment-options"></a>选择评估选项

1. 选择你打算迁移到目标 SQL Server 版本。

2. 选择报表类型。

   时进行评估源 SQL Server 实例迁移到本地 SQL Server 或 SQL Server 托管在 Azure VM 的目标上，可以选择一个或两个以下的评估报告类型：

    -   **兼容性问题**
    -   **新功能的建议**

    ![选择 SQL Server 目标的评估报表类型](../dma/media/AssessmentTypes.png)

   当评估源 SQL Server 实例迁移到 Azure SQL 数据库，可以选择一个或两个以下的评估报告类型：

    -   **检查数据库兼容性**
    -   **检查功能奇偶一致性**

    ![选择 SQL 数据库目标的评估报表类型](../dma/media/AssessmentTypes_Azure.png)

## <a name="add-databases-to-assess"></a>添加要评估的数据库

1.  选择**添加源**以打开连接飞出式菜单。

2.  输入 SQL server 实例名称，选择身份验证类型、 设置正确的连接属性，并选择**Connect**。

3.  选择要评估和选择的数据库**添加**。

    > [!NOTE] 
    > 您可以通过选择它们时按住 Shift 或 Ctrl 键，并单击删除多个数据库**删除源**。 您还可以添加数据库来自多个 SQL Server 实例使用**添加源**按钮。

4.  单击**下一步**，开始评估。

    ![添加源和启动评估](../dma/media/SelectDatabase.png)

## <a name="view-results"></a>查看结果

评估的持续时间取决于添加的数据库数目和每个数据库的架构大小。 只要提供了它们，结果将显示每个数据库。

1.  选择已完成评估，该数据库，然后在之间切换**兼容性问题**并**功能建议**使用切换器。

2.  跨所有兼容性级别受目标 SQL Server 版本上选择查看兼容性问题**选项**页。

你可以通过分析受影响的对象，其详细信息，并可能下标识每个问题的修复程序中查看兼容性问题**重大更改**，**的行为更改**，和**已弃用的功能**。

![查看评估结果](../dma/media/ReviewResults.png)

同样，可以查看功能建议跨**性能**，**存储**，并**安全**区域。

功能推荐涵盖大量的内存中 OLTP、 列存储、 Stretch Database、 Always Encrypted、 动态数据掩码和透明数据加密等功能。

![查看功能建议](../dma/media/FeatureRecommendations.png)

对于 Azure SQL 数据库，评估提供迁移阻塞问题和功能奇偶校验问题。 通过选择特定选项来查看这两个类别的结果。

- **SQL Server 功能奇偶校验**类别提供了全面的建议，在 Azure 中和缓解步骤中可用的替代方法。 它可帮助你规划在迁移项目中的这项工作。

  ![查看 SQL Server 功能奇偶一致性的信息](../dma/media/SQLFeatureParity.png)

- **兼容性问题**类别提供部分支持或不受支持的功能，能够阻止在本地 SQL Server 数据库迁移到 Azure SQL 数据库。 然后，它提供了建议，以帮助你解决这些问题。

  ![查看兼容性问题](../dma/media/CompatibilityIssues.png)

## <a name="export-results"></a>导出结果

所有数据库都完成评估后，选择**将报表导出**将结果导出到 JSON 文件或 CSV 文件。 然后可以在自己方便时分析数据。

可以同时运行多个评估并查看评估的状态，方法是打开**所有评估**页。
