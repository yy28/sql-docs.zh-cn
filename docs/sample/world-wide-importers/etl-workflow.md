---
title: "ETL 工作流 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- samples
ms.custom: 
ms.date: 06/15/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 679e58fe-b062-4934-a94c-9bb916b0bcb0
caps.latest.revision: 5
author: BarbKess
ms.author: barbkess
manager: jhubbard
robots: noindex,nofollow
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 85898dfc3a12ee195910bf965f0099b35f95b239
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="wideworldimportersdw-etl-workflow"></a>WideWorldImportersDW ETL 工作流
ETL 包 WWI_Integration 用于将数据从 WideWorldImporters 数据库迁移到 WideWorldImportersDW 数据库，数据发生更改。 定期运行包 （通常每天一次）。

## <a name="overview"></a>概述

设计的包使用 SQL Server Integration Services (SSIS) 来安排大容量 T-SQL 的操作 （而不是 SSIS 内的单独转换） 以确保高性能。

跟事实数据表首先，加载维度。 可以随时在出现故障后重新运行包。

工作流如下所示：

 ![WideWorldImporters ETL 工作流](../../sample/world-wide-importers/media/wideworldimporters-etl-workflow.png)

它启动时使用表达式的任务可适当的截止时间。 此时间是当前时间更少的几分钟时间。 （这将比请求数据从右到当前时间更可靠。） 然后，它将截断时间中的任何毫秒。

主处理启动通过填充日期维度表。 它可确保所有日期为当前年份，已经都填充表中。

此后，数据流任务的一系列加载每个维度，则每个事实。

## <a name="prerequisites"></a>必要條件

- SQL Server 2016 （或更高版本） 与数据库 WideWorldImporters 和 WideWorldImportersDW。 这可能是在相同或不同的 SQL Server 实例上。
- SQL Server Management Studio (SSMS)
- SQL Server 2016 Integration Services (SSIS)。
  - 请确保你已创建 SSIS 目录。 否则，请右键单击**Integration Services**在 SSMS 对象资源管理器，然后选择**添加目录**。 遵循的默认值。 它将要求你启用 sqlclr 并提供一个密码。


## <a name="download"></a>下载

最新版本中的示例：

[wide world 导入程序版本](http://go.microsoft.com/fwlink/?LinkID=800630)

下载 SSIS 包文件**每日 ETL.ispac**。

从以下位置提供了源代码以重新创建示例数据库。

[wide world importers 计划](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl)

## <a name="install"></a>Install

1. 部署 SSIS 包。
   - 从 Windows 资源管理器中打开"每日 ETL.ispac"包。 这将启动 Integration Services 部署向导。
   - 在"选择源"下具有指向"每日 ETL.ispac"包路径中点击默认项目部署。
   - 在"选择目标"下，输入承载 SSIS 目录的服务器的名称。
   - 选择 SSIS 目录，例如在一个新文件夹"WideWorldImporters"下的路径。
   - 通过单击部署完成向导。

2. 创建 ETL 过程的 SQL Server 代理作业。
   - 在 SSMS 中，右键单击"SQL Server 代理"，并选择新建-> 作业。
   - 选择的名称，例如"WideWorldImporters ETL"。
   - 添加一个作业步骤的类型"SQL Server Integration Services 包"。
   - 选择将服务器与 SSIS 目录中，然后选择"每日 ETL"包。
   - 在配置-> 连接管理器确保正确配置的源和目标的连接。 默认值是连接到本地实例。
   - 单击确定以创建作业。

3. 执行或计划作业。

