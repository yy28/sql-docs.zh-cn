---
title: 广域国际进口商DW - ETL工作流程 |微软文档
description: 将 ETL 包与 SQL 服务器集成服务 （SSIS） 一起定期将数据从广域世界导入者数据库迁移到广域世界导入者DW。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 98ce2b9aa11b2e1381da1f16455df8a2c0d3f243
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487426"
---
# <a name="wideworldimportersdw-etl-workflow"></a>广域国际进口商DW ETL工作流程
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
使用*WWI_Integration* ETL 包将数据从宽世界进口商数据库迁移到 WideWorld导入者DW 数据库，因为数据发生更改。 包定期运行（通常每天）。

该包通过使用 SQL Server 集成服务来协调批量 T-SQL 操作（而不是在集成服务中进行单独的转换），从而确保高性能。

首先加载维度，然后加载事实表。 在发生故障后，您可以随时重新运行包。

工作流如下所示：

 ![广域国际进口商 ETL 工作流程](media/wide-world-importers/wideworldimporters-etl-workflow.png)

工作流从确定适当截止时间的表达式任务开始。 截止时间是当前时间减去几分钟。 （此方法比直接请求数据到当前时间更可靠。任何毫秒都从时间被截断。

主处理首先填充日期维度表。 处理可确保在表中填充了当前年份的所有日期。

接下来，一系列数据流任务加载每个维度。 然后，它们加载每个事实。

## <a name="prerequisites"></a>先决条件

- SQL Server 2016（或更高版本），具有宽世界导入器和广域国际导入器DW数据库（在 SQL 服务器的相同或不同情况下）
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - 确保创建集成服务目录。 要创建集成服务目录，请在 SQL 服务器管理工作室对象资源管理器中，右键单击**集成服务**，然后选择"**添加目录**"。 保留默认选项。 系统将提示您启用 SQLCLR 并提供密码。


## <a name="download"></a>下载

有关该示例的最新版本，请参阅[全球进口商版本](https://go.microsoft.com/fwlink/?LinkID=800630)。 下载*每日 ETL.ispac*集成服务包文件。

有关重新创建示例数据库的源代码，请参阅[全球导入者](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-ssis)。

## <a name="install"></a>安装

1. 部署集成服务包：
   1. 在 Windows 资源管理器中，打开*每日 ETL.ispac*包。 这将启动 SQL 服务器集成服务部署向导。
   2. 在 **"选择源**"下，按照项目部署的默认值操作，路径指向每日*ETL.ispac*包。
   3. 在 **"选择目标**"下，输入承载集成服务目录的服务器的名称。
   4. 在集成服务目录下选择路径，例如，在名为*WideWorld 导入器*的新文件夹中选择路径。
   5. 选择 **"部署"** 以完成向导。

2. 为 ETL 进程创建 SQL 服务器代理作业：
   1. 在管理工作室中，右键单击**SQL 服务器代理**，然后选择 **"新** > **作业**"。
   2. 输入名称，例如，*宽世界进口商 ETL*。
   3. 添加**SQL 服务器集成服务包**类型的**作业步骤**。
   4. 选择具有集成服务目录的服务器，然后选择*每日 ETL*包。
   5. 在**配置** > **连接管理器**下，确保正确配置到源和目标的连接。 默认值是连接到本地实例。
   6. 选择 **"确定"** 以创建作业。

3. 执行或安排作业。
