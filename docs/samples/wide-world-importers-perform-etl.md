---
title: WideWorldImportersDW-ETL 工作流 |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 36638c4cc2bda58ac277822d5c4a4ce5421ab8b4
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38066525"
---
# <a name="wideworldimportersdw-etl-workflow"></a>WideWorldImportersDW ETL 工作流
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
使用*WWI_Integration* ETL 包，以将数据从 WideWorldImporters 数据库迁移到 WideWorldImportersDW 数据库，随着数据的更改。 定期运行包 （通常每日）。

包可确保通过使用 SQL Server Integration Services 安排 T-SQL 的大容量操作 （而不是在 Integration Services 中的单独转换） 的高性能。

首先，加载维度，并随后加载事实数据表。 在出现故障后的任何时间，可以重新运行包。

工作流如下所示：

 ![WideWorldImporters ETL 工作流](media/wide-world-importers/wideworldimporters-etl-workflow.png)

在工作流启动使用表达式的任务，用于确定适当的截止时间。 截止时间是当前时间减几分钟时间。 （这种方法是比请求的数据从右到当前时间更可靠。）任何毫秒为单位的时间将被截断。

主处理首先会填充日期维度表。 在处理可确保，已在表中填充了当前年份的所有日期。

接下来，一系列的数据流任务加载每个维度。 然后，它们的加载每个事实。

## <a name="prerequisites"></a>必要條件

- SQL Server 2016 （或更高版本），与 WideWorldImporters 和 WideWorldImportersDW 数据库 （在相同或不同的 SQL Server 实例）
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - 请确保创建的 Integration Services 目录。 若要创建的 Integration Services 目录，在 SQL Server Management Studio 对象资源管理器中，右键单击**Integration Services**，然后选择**添加目录**。 保留默认选项。 系统会提示启用 SQLCLR 和提供密码。


## <a name="download"></a>下载

该示例的最新版本，请参阅[wide world 导入程序版本](http://go.microsoft.com/fwlink/?LinkID=800630)。 下载*每日 ETL.ispac* Integration Services 包文件。

若要重新创建示例数据库的源代码，请参阅[wide world importers](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-integration-etl)。

## <a name="install"></a>Install

1. 部署 Integration Services 包：
   1. 在 Windows 资源管理器中打开*每日 ETL.ispac*包。 这将启动 SQL Server Integration Services 部署向导。
   2. 下**选择源**，为项目部署遵循的默认值指向的路径*每日 ETL.ispac*包。
   3. 下**选择目标**，输入托管 Integration Services 目录的服务器的名称。
   4. 例如，名为的新文件夹中选择 Integration Services 目录下的路径*WideWorldImporters*。
   5. 选择**部署**以完成该向导。

2. 创建 ETL 过程的 SQL Server 代理作业：
   1. 在 Management Studio 中，右键单击**SQL Server 代理**，然后选择**新建** > **作业**。
   2. 例如，输入一个名称， *WideWorldImporters ETL*。
   3. 添加**作业步骤**类型的**SQL Server Integration Services 包**。
   4. 选择具有 Integration Services 目录的服务器，然后选择*日常 ETL*包。
   5. 下**配置** > **连接管理器**，确保正确配置的源和目标的连接。 默认值是连接到本地实例。
   6. 选择**确定**创建作业。

3. 执行或计划作业。
