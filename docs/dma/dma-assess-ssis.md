---
title: 执行 SQL Server Integration Service 迁移评估 (数据迁移助手) |Microsoft Docs
description: 了解如何使用数据迁移助手在迁移到 Azure SQL 数据库或 Azure SQL 数据库托管实例之前评估本地 SQL Server 集成服务
ms.custom: ''
ms.date: 08/23/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 14e53b3820e784916484cbe6a15ba82cd2ed5c8e
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2019
ms.locfileid: "70001369"
---
# <a name="perform-a-sql-server-integration-service-migration-assessment-with-data-migration-assistant"></a>使用数据迁移助手执行 SQL Server Integration Service 迁移评估

下面的分步说明将帮助你使用数据迁移助手执行将 SQL Server Integration Service (SSIS) 包迁移到 Azure SQL 数据库或 Azure SQL 数据库托管实例的第一个评估。

## <a name="create-an-assessment"></a>创建评估

1. 选择 "**新建**(+)" 图标, 然后选择 "**评估**" 项目类型作为 " **Integration Service**"。

1. 设置源和目标服务器类型。

    选择 "源" 作为 " **SQL Server**", 并将 "目标服务器类型" 设置为 " **azure sql 数据库**" 或 " **azure sql 数据库托管实例**"。

1. 单击 **“创建”** 。

    ![创建评估](media/dma-assess-ssis/dma-assess-ssis-create.png)

## <a name="add-sources-to-assess"></a>添加要评估的源

1. 遵循默认选项, 然后单击 "**下一步**" "**选择源**"。

1. 输入 SQL server 实例名称, 选择 "身份验证类型", 设置正确的连接属性。
1. 输入包含 SSIS 包的文件夹路径
1. 如果适用, 请输入包加密密码, 然后**连接**。
1. 选择要评估的文件系统, 然后选择 "**添加**"。
  ![添加源](media/dma-assess-ssis/dma-assess-ssis-addsource.png)
1. 如果需要评估多个文件夹, 请选择 "**添加源**" 以打开 "连接" 弹出菜单。
1. 单击 "**启动评估**"。
  ![开始评估](media/dma-assess-ssis/dma-assess-ssis-assess.png)

## <a name="view-results"></a>查看结果

兼容性问题类别提供部分支持或不支持的功能, 这些功能会阻止将本地 SSIS 包迁移到 Azure-SSIS Integration Runtime。 然后, 它提供了帮助你解决这些问题的建议。

![查看结果](media/dma-assess-ssis/dma-assess-ssis-result.png)

## <a name="next-steps"></a>后续步骤

- [将 SQL Server Integration Services 包迁移到 Azure SQL 数据库托管实例](https://docs.microsoft.com/en-us/azure/dms/how-to-migrate-ssis-packages-managed-instance)
- [将 SQL Server Integration Services 包重新部署到 Azure SQL 数据库](https://docs.microsoft.com/en-us/azure/dms/how-to-migrate-ssis-packages)
