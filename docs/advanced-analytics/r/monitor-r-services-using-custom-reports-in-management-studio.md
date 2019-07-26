---
title: 使用 Management Studio 中的自定义报表监视 R Services
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: effcfe458fc004fd8fb44bb58095e91a2fb56b8d
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470070"
---
# <a name="monitor-machine-learning-services-using-custom-reports-in-management-studio"></a>使用 Management Studio 中的自定义报表监视机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

为了更轻松地管理用于机器学习的实例, 产品团队提供了许多可添加到 SQL Server Management Studio 的示例自定义报表。 在这些报表中, 可以查看详细信息, 例如:

- 活动 R 或 Python 会话
- 实例的配置设置
- 机器学习作业的执行统计信息
- R Services 的扩展事件
- 当前实例上安装的 R 或 Python 包

本文介绍如何安装和使用专门为计算机 leaerning 提供的自定义报表。 

有关 Management Studio 中的报表的常规介绍, 请参阅[Management Studio 中的自定义报表](../../ssms/object/custom-reports-in-management-studio.md)。

## <a name="how-to-install-the-reports"></a>如何安装报表

报表使用 SQL Server Reporting Services 进行设计，但可通过 SQL Server Management Studio 直接使用（即使实例上未安装 Reporting Services）。 

若要使用这些报表，请：

* 从 SQL Server 产品示例的 GitHub 存储库中下载 RDL 文件。
* 将文件添加到 SQL Server Management Studio 使用的自定义报表文件夹。
* 在 SQL Server Management Studio 中打开报表。


### <a name="step-1-download-the-reports"></a>步骤 1. 下载报表

1. 打开包含[SQL Server 产品示例](https://github.com/Microsoft/sql-server-samples)的 GitHub 存储库, 并下载示例报表。 

    + [SSMS 自定义报告](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)

    > [!NOTE]
    > 报表可与 SQL Server 2017 Machiine Learning Services 一起使用, 也可与 SQL Server 2016 R Services 一起使用。

2. 若要下载示例，还可登录到 GitHub 并设置示例的本地分叉。 

### <a name="step-2-copy-the-reports-to-management-studio"></a>步骤 2. 将报表复制到 Management Studio

3. 找到 SQL Server Management Studio 使用的自定义报表文件夹。 自定义报表默认存储在此文件夹中：
    
   `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

   但是，可指定其他文件夹或创建子文件夹。

4. 将 *.RDL 文件复制到自定义报表文件夹。


### <a name="step-3-run-the-reports"></a>步骤 3. 运行报表

5. 在 Management Studio 中，右键单击要在其中运行报表的示例的“数据库”  节点。
6. 单击“报表” ，然后单击“自定义报表” 。
7. 在“打开文件”  对话框中，找到自定义报表文件夹。
8. 选择某个下载的 RDL 文件，然后单击“打开” 。

> [!IMPORTANT]
> 这些报表在某些计算机（例如具有高 DPI 或分辨率大于 1080p 的显示设备）或某些远程桌面会话中无法使用。 SSMS 的报表查看器控件中存在 bug，它会导致报表崩溃。

## <a name="report-list"></a>报表列表

GitHub 中的产品示例存储库当前包含以下报表:

+ **R Services - 活动会话**

  使用此报表来查看当前连接到 SQL Server 实例并运行机器学习作业的用户。 
  
+ **R Services - 配置**

  使用此报表查看外部脚本运行时和相关服务的配置。 报表将指示是否需要重启，并检查所需的网络协议。 
  
  在 SQL Server 中运行的机器学习任务需要使用默示身份验证作为计算上下文。 若要验证是否已配置隐含身份验证, 该报告将验证是否存在组 SQLRUserGroup 的数据库登录名。

 + **R Services - 配置实例** 

   此报告旨在帮助你配置机器学习。 您还可以运行此报表来修复前面报表中发现的配置错误。
 
+ **R Services - 执行统计信息**

  使用此报表查看机器学习作业的执行统计信息。 例如，可获取执行的 R 脚本总数、并行执行数，以及最常用的 RevoScaleR 函数。 单击 "**查看 SQL 脚本**" 以获取此报表后面的完整 t-sql 代码。

  目前，报表仅监视 RevoScaleR 包函数的统计信息。

+ **R Services - 扩展事件**

  使用此报表可以查看可用于监视与外部脚本运行时相关的任务的扩展事件的列表。 单击 "**查看 SQL 脚本**" 以获取此报表后面的完整 t-sql 代码。

+ **R Services - 包**

  使用此报表查看 SQL Server 实例上安装的 R 或 Python 包的列表。

+ **R Services - 资源使用情况**

  使用此报告可以通过外部脚本执行来查看 CPU、内存和 i/o 资源的消耗情况。 还可查看外部资源池的内存设置。

## <a name="see-also"></a>请参阅

[监视服务](managing-and-monitoring-r-solutions.md)

[R Services 的扩展事件](extended-events-for-sql-server-r-services.md)
