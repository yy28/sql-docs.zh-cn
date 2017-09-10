---
title: "使用 Management Studio 中的自定义报表监视 R Services | Microsoft Docs"
ms.custom: 
ms.date: 02/20/2017
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
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 14f6d6d7373afd452f06acae43f7023de136bc71
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="monitor-r-services-using-custom-reports-in-management-studio"></a>使用 Management Studio 中的自定义报表监视 R Services
为简化 SQL Server R Services 的管理，产品团队提供了大量示例自定义报表，可将其添加到 SQL Server Management Studio 以查看 R Services 的详细信息，例如：

- 活动 R 会话的列表
- 当前实例的 R 配置
- R 运行时的执行统计信息
- R Services 的扩展事件列表
- 当前示例上安装的 R 包列表

本主题介绍了报表的安装和使用方式。 若要深入了解 Management Studio 中的自定义报表，请参阅 [Management Studio 中的自定义报表](~/ssms/object/custom-reports-in-management-studio.md)。

## <a name="how-to-install-the-reports"></a>如何安装报表

报表使用 SQL Server Reporting Services 进行设计，但可通过 SQL Server Management Studio 直接使用（即使实例上未安装 Reporting Services）。 

若要使用这些报表，请：

* 从 SQL Server 产品示例的 GitHub 存储库中下载 RDL 文件。
* 将文件添加到 SQL Server Management Studio 使用的自定义报表文件夹。
* 在 SQL Server Management Studio 中打开报表。


### <a name="step-1-download-the-reports"></a>步骤 1. 下载报表

1. 打开包含 [SQL Server 产品示例](https://github.com/Microsoft/sql-server-samples)的 GitHub 存储库，并从此页下载示例报表： 

   + [SSMS 自定义报告](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/r-services/ssms-custom-reports)
      
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

GitHub 中的产品示例存储库目前包括下列 SQL Server R Services报表：

+ **R Services - 活动会话**

  使用此报表查看当前连接到 SQL 示例和运行 R 作业的用户。 
  
+ **R Services - 配置**

  使用此报表查看 R 运行时的属性和 R Services 的配置。 报表将指示是否需要重启，并检查所需的网络协议。 
  
  在 SQL 计算上下文中运行 R 需要隐式身份验证。为检查此项，报表将验证是否存在面向组 SQLRUserGroup 的数据库登录名。

  > [!NOTE]
  > 若要深入了解这些字段，请参阅 Hadley Wickam 编写的 [Package metadata](http://r-pkgs.had.co.nz/description.html)（包源数据）。 例如，已引入 R 运行时的“别名”  字段，帮助区分不同版本。 

 + **R Services - 配置实例** 

   此报表旨在帮助你在安装后配置 R Services。 如果 R Services 配置错误，可从上述报表中运行它。
 
+ **R Services - 执行统计信息**

  使用此报表查看 R Services 的执行统计信息。 例如，可获取执行的 R 脚本总数、并行执行数，以及最常用的 RevoScaleR 函数。
  目前，报表仅监视 RevoScaleR 包函数的统计信息。
  单击“查看 SQL 脚本”  ，获取此报表的 T-SQL 代码。 

+ **R Services - 扩展事件**

  使用此报表查看可用于监视 R 脚本执行的扩展事件列表。 
  单击“查看 SQL 脚本”  ，获取此报表的 T-SQL 代码。

+ **R Services - 包**

  使用此报表查看 SQL Server 实例上安装的 R 包的列表。 目前，此报表包括以下包属性： 
  + 包（名称）
  + 版本 
  + 依赖的对象
  + 许可证
  + 生成
  + Lib 路径

+ **R Services - 资源使用情况**

  使用此报表查看 SQL Server R 脚本执行的 CPU、内存和 I/O 资源占用情况。 还可查看外部资源池的内存设置。 


## <a name="see-also"></a>另请参阅

[监视 R Services](../../advanced-analytics/r-services/monitoring-r-services.md)

[R Services 的扩展事件](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md)


