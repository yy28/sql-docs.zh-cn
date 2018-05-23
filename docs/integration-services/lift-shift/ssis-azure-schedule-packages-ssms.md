---
title: 使用 SSMS 计划 Azure 中的 SSIS 包 | Microsoft Docs
description: 介绍如何在 SQL Server Management Studio (SSMS) 中使用 Schedule 命令计划部署到 Azure SQL 数据库的 SSIS 包。
ms.date: 05/09/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.component: lift-shift
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 72b20d4d42517555449f639cee398db4363d5735
ms.sourcegitcommit: 0cc2cb281e467a13a76174e0d9afbdcf4ccddc29
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2018
---
# <a name="schedule-the-execution-of-an-ssis-package-in-azure-with-sql-server-management-studio-ssms"></a>在 SQL Server Management Studio (SSMS) 中计划 Azure 中的 SSIS 包执行

SQL Server Management Studio (SSMS) 可为部署到 Azure SQL 数据库的 SSIS 包提供计划功能。 本地 SQL Server 和 SQL 数据库托管实例（预览版）分别包含 SQL Server 代理和托管实例代理作为一级 SSIS 作业计划程序。 另一方面，SQL 数据库没有内置的一级 SSIS 作业计划程序。 本文介绍的 SSMS 功能提供类似于 SQL Server 代理的熟悉用户界面，用于计划部署到 SQL 数据库的包。

如果要使用 SQL 数据库托管 SSIS 目录数据库 `SSISDB`，可使用此 SSMS 功能生成计划 SSIS 包所需的数据工厂管道、活动和触发器。 然后可在数据工厂中编辑和扩展这些对象。

如果使用 SSMS 来计划包，SSIS 会自动创建三个基于所选包和时间戳的名称命名的新数据工厂对象。 例如，如果 SSIS 包的名称为 MyPackage，SSMS 将创建与以下类似的新数据工厂对象：

| Object | “属性” |
|---|---|
| 管道 | Pipeline_MyPackage_2018-05-08T09_00_00Z |
| 执行 SSIS 包活动 | Activity_MyPackage_2018-05-08T09_00_00Z |
| 触发器 | Trigger_MyPackage_2018-05-08T09_00_00Z |
|||

## <a name="prerequisites"></a>必备条件

本文介绍的功能要求 SQL Server Management Studio 17.7 或更高版本。 若要获取 SSMS 最新版本，请参阅[下载 SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)。

## <a name="schedule-a-package-in-ssms"></a>在 SSMS 中计划包

1. 在 SSMS 的对象资源管理器中，依次选择 SSISDB 数据库、文件夹、项目和包。 右键单击包，然后选择“计划”。

    ![选择要计划的包。](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image1-schedule.png)

2. “新建计划”对话框随即打开。 在“新建计划”对话框的“常规”页中，提供新计划作业的名称和说明。

    ![“新建计划”对话框的“常规”页](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image2-new-schedule.png)

3. 在“新建计划”对话框的“包”页中，选择可选运行时设置和运行时环境。

    ![“新建计划”对话框的“包”页](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image3-new-schedule2.png)

4. 在“新建计划”对话框的“计划”页中，提供计划设置（如频率、当日时间和持续时间）。

    ![“新建计划”对话框的“计划”页](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image4-new-schedule3.png)

5. 在“新建计划”对话框中完成创建作业后，将显示一条确认信息，提醒你 SSMS 要创建的新数据工厂对象。 如果在确认对话框中选择“是”，Azure 门户中将打开新的数据工厂管道，以便查看和自定义。

    ![确认新计划](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image5-confirmation.png)

6. 若要自定义计划触发器，从“触发器”菜单中选择“新建/编辑”。

    ![选择性地编辑新管道](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image6-edit.png)

    “编辑触发器”边栏选项卡随即打开，以便自定义计划选项。

    ![编辑触发器](media/ssis-azure-schedule-packages-ssms/schedule-ssms-image7-edit2.png)

## <a name="next-steps"></a>后续步骤

若要了解用于计划 SSIS 包的其他方法，请参阅[计划 Azure 上 SSIS 包的执行](ssis-azure-schedule-packages.md)。

若要了解有关 Azure 数据工厂、管道、活动和触发器的详细信息，请参阅下列文章：
-   [Azure 数据工厂中的管道和活动](https://docs.microsoft.com/azure/data-factory/concepts-pipelines-activities)
-   [Azure 数据工厂中的管道执行和触发器](https://docs.microsoft.com/azure/data-factory/concepts-pipeline-execution-triggers)
