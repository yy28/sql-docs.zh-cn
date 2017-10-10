---
title: "使用 Management Studio 中的自定义报表监视 R Services | Microsoft Docs"
ms.custom: 
ms.date: 10/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5933c72c-ba63-4966-b882-75719ef8428e
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 5a1990a7612eab44029c36129e73050854337930
ms.contentlocale: zh-cn
ms.lasthandoff: 10/10/2017

---
# <a name="monitor-machine-learning-services-using-custom-reports-in-management-studio"></a>监视在 Management Studio 中使用自定义报表的机器学习服务

若要更加轻松地管理用于机器学习的实例，产品团队提供了一些示例自定义报表，你可以将其添加到 SQL Server Management Studio。 在这些报表，你可以如查看详细信息：

- 活动 R 或 Python 会话
- 实例的配置设置
- 机器学习作业的执行统计信息
- R Services 的扩展的事件
- 当前实例上安装的 R 或 Python 包

此文章介绍了如何安装和使用专门为机 leaerning 提供的自定义报表。 

在 Management Studio 中的报表的常规介绍，请参阅[Management Studio 中的自定义报表](../../ssms/object/custom-reports-in-management-studio.md)。

## <a name="how-to-install-the-reports"></a>如何安装报表

报表使用 SQL Server Reporting Services 进行设计，但可通过 SQL Server Management Studio 直接使用（即使实例上未安装 Reporting Services）。 

若要使用这些报表，请：

* 从 SQL Server 产品示例的 GitHub 存储库中下载 RDL 文件。
* 将文件添加到 SQL Server Management Studio 使用的自定义报表文件夹。
* 在 SQL Server Management Studio 中打开报表。


### <a name="step-1-download-the-reports"></a>步骤 1. 下载报表

1. 打开包含 GitHub 存储库[SQL Server 产品示例](https://github.com/Microsoft/sql-server-samples)，并下载示例报表。 

    + [SSMS 自定义报表](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)

    > [!NOTE]
    > 可以与 SQL Server 自 2017 年 Machiine 学习服务或 SQL Server 2016 R Services 使用报表。

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

在 GitHub 中的产品示例存储库当前包括以下报表：

+ **R Services - 活动会话**

  使用此报表以查看当前连接到 SQL Server 实例，并运行机器学习作业的用户。 
  
+ **R Services - 配置**

  使用此报表以查看外部脚本运行时和相关的服务的配置。 报表将指示是否需要重启，并检查所需的网络协议。 
  
  默示身份验证时需要在 SQL Server 作为计算上下文中运行的机器学习任务。 若要验证配置默示身份验证，该报表，请验证组 SQLRUserGroup 是否存在数据库登录名。

 + **R Services - 配置实例** 

   此报表旨在帮助你配置机器学习。 你还可以运行此报表以修复在前面的报表中找到的配置错误。
 
+ **R Services - 执行统计信息**

  使用此报表以查看机学习作业的执行统计信息。 例如，可获取执行的 R 脚本总数、并行执行数，以及最常用的 RevoScaleR 函数。 单击**查看 SQL 脚本**若要获取完整的 T-SQL 代码隐藏此报表。

  目前，报表仅监视 RevoScaleR 包函数的统计信息。

+ **R Services - 扩展事件**

  使用此报表以查看可用于监视与外部脚本运行时相关的任务的扩展事件的列表。 单击**查看 SQL 脚本**若要获取完整的 T-SQL 代码隐藏此报表。

+ **R Services - 包**

  使用此报表以查看 SQL Server 实例上安装的 R 或 Python 软件包的列表。

+ **R Services - 资源使用情况**

  使用此报表可以查看的消耗 CPU、 内存和 I/O 资源通过外部脚本执行。 还可查看外部资源池的内存设置。

## <a name="see-also"></a>另请参阅

[监视 R Services](../../advanced-analytics/r-services/monitoring-r-services.md)

[R Services 的扩展事件](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md)

