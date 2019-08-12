---
title: 在 Azure Data Studio 中提交 SQL Server 大数据群集上的 Spark 作业
titleSuffix: SQL Server big data clusters
description: 在 Azure Data Studio 中提交 SQL Server 大数据群集上的 Spark 作业。
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6731a753c643512cd05dbc9d7b7de2c9a064576f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68470666"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-clusters-in-azure-data-studio"></a>在 Azure Data Studio 中提交 SQL Server 大数据群集上的 Spark 作业

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

大数据群集的关键方案之一是能够为 SQL Server 2019 预览版提交 Spark 作业。 使用 Spark 作业提交功能，你可以提交引用 SQL Server 2019 大数据群集的的本地 Jar 或 Py 文件。 它还允许你执行已经位于 HDFS 文件系统中的 Jar 或 Py 文件。 

## <a name="prerequisites"></a>必备条件

- [SQL Server 2019 大数据工具](deploy-big-data-tools.md)：
   - **Azure Data Studio**
   - **SQL Server 2019 扩展**
   - **kubectl**

- [将 Azure Data Studio 连接到大数据群集的 HDFS/Spark 网关](connect-to-big-data-cluster.md)。

## <a name="open-spark-job-submission-dialog"></a>打开 Spark 作业提交对话框

可以通过多种方式打开 Spark 作业提交对话框。 其中包括仪表板、对象资源管理器中的上下文菜单和命令面板。

- 若要打开 Spark 作业提交对话框，请单击仪表板中的“新建 Spark 作业”  。

    ![通过单击仪表板打开提交菜单](./media/submit-spark-job/new-spark-job.png)

- 或者在对象资源管理器中右键单击群集，然后从上下文菜单中选择“提交 Spark 作业”  。

    ![通过右键单击文件打开提交菜单](./media/submit-spark-job/submit-spark-job-1.png)


- 若要打开预填充了 Jar/Py 字段的 Spark 作业提交对话框，请在对象资源管理器中右键单击某个 Jar/Py 文件，然后从上下文菜单中选择“提交 Spark 作业”  。  

    ![通过右键单击群集打开提交菜单](./media/submit-spark-job/submit-spark-job.png)

- 通过键入“Ctrl+Shift+P”（在 Windows 中）和“Cmd+Shift+P”（在 Mac 中），从命令面板中使用“提交 Spark 作业”    。

    ![Windows 中的提交菜单命令面板](./media/submit-spark-job/submit-spark-job-3.png)

    ![Mac 中的提交菜单命令面板](./media/submit-spark-job/submit-spark-job-4.png)
  
 
## <a name="submit-spark-job"></a>提交 Spark 作业 

Spark 作业提交对话框如下所示。 输入作业名称、JAR/Py 文件路径、主类和其他字段。 Jar/Py 文件源可以来自本地或 HDFS。 如果 Spark 作业引用了 Jar、Py 文件或其他文件，请单击“高级”选项卡并输入相应的文件路径  。 单击“提交”以提交 Spark 作业  。

![新建 spark 作业对话框](./media/submit-spark-job/submit-spark-job-section.png)

![高级对话框](./media/submit-spark-job/submit-spark-job-section-1.png)

## <a name="monitor-spark-job-submission"></a>监视 Spark 作业提交

提交 Spark 作业后，Spark 作业提交和执行状态信息显示在左侧的“任务历史记录”中。 有关进度和日志的详细信息也显示在底部的“输出”窗口中  。

- 当 Spark 作业正在进行时，“任务历史记录”面板和“输出”窗口会刷新进度   。

    ![监视正在进行的 spark 作业](./media/submit-spark-job/monitor-spark-job-submission.png)

- 当 Spark 作业成功完成后，Spark UI 和 Yarn UI 链接显示在“输出”窗口中  。 单击链接可获取详细信息。

    ![输出中的 Spark 作业链接](./media/submit-spark-job/monitor-spark-job-submission-2.png)

## <a name="next-steps"></a>后续步骤

有关 SQL Server 大数据群集和相关方案的详细信息，请参阅[什么是 SQL Server 大数据群集？](big-data-cluster-overview.md)