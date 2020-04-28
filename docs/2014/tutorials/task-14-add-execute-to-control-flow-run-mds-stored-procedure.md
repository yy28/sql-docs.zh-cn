---
title: 任务14：将执行 SQL 任务添加到控制流以运行 MDS 的存储过程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 9a5d1b52-d505-4e6f-8a89-569329c094e2
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8c926f2ea3d9ef9973f75764e254c5e0884836e3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "78177287"
---
# <a name="task-14-adding-execute-sql-task-to-control-flow-to-run-the-stored-procedure-for-mds"></a>任务 14：将执行 SQL 任务添加到控制流以运行 MDS 的存储过程
  在将数据加载到 MDS 的临时表后，您运行与该表相关联的存储过程以便将数据从临时表加载到 MDS 数据库的相应表中。 此存储过程有两个需要传递的必需参数：LogFlag 和 VersionName。 LogFlag 指定在临时过程中是否将事务记入日志，而 VersionName 表示模型版本。 有关更多详细信息，请参阅[分步存储过程](https://msdn.microsoft.com/library/hh231028.aspx)主题。

 在本任务中，您将执行 SQL 任务添加到控制流中，以便调用该存储过程来将临时数据加载到相应 MDS 表中。

1.  现在，切换到 "**控制流**" 选项卡。

2.  将 "**执行 SQL 任务**" 从 " **SSIS 工具箱**" 拖放到 "**控制流**" 选项卡。

3.  右键单击 "**控制流**" 选项卡中的 "**执行 SQL 任务**"，然后单击 "**重命名**"。 键入 "**触发器存储过程" 将数据加载到 MDS 中**，然后按**enter**。

4.  使用绿色连接器将**接收、清理、匹配和组织供应商数据**连接到**触发器存储过程以加载数据**。

     ![连接以执行 SQL 任务](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-01.jpg "连接以执行 SQL 任务")

5.  使用 "**变量**" 窗口，添加两个具有以下设置的新变量。 如果看不到 "**变量**" 窗口，请单击菜单栏上的 " **SSIS** " 并单击 "**变量**"。

    |名称|数据类型|值|
    |----------|---------------|-----------|
    |LogFlag|Int32|1|
    |VersionName|字符串|VERSION_1|

     ![SSIS 变量窗口](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-02.jpg "SSIS 变量窗口")

6.  双击 "**触发器存储过程" 将数据加载到 MDS 中**。

7.  在 "**执行 SQL 任务编辑器**" 对话框中，选择 " **（本地）"。MDS** （或**localhost。MDS**）进行**连接**。

8.  键入**EXEC [stg.<name]. [udp_Supplier_Leaf]?,?,?** 用于**SQL 语句**。 您可以使用 SQL Server Management Studio 确认该名称。

     ![“执行 SQL 编辑器”对话框 - 常规设置](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-03.jpg "“执行 SQL 编辑器”对话框 - 常规设置")

9. 单击左侧菜单中的 "**参数映射**"。

10. 在 "**参数映射**" 页中，单击 "**添加**" 以添加映射。 最大化该窗口并且调整列大小，以便您可以正确在下拉列表中看到值。

11. 从 "**变量名称**" 的下拉列表中选择 " **User：： VersionName** "。

12. 为 "**数据类型**" 选择 " **NVARCHAR** "。

13. 输入**0** （零）作为**参数名称**。

14. 重复执行前四个步骤以便再添加两个变量。

    |变量名|数据类型（重要）|参数名称|
    |-------------------|-----------------------------|--------------------|
    |User::LogFlag|LONG|1|
    |User::BatchTag|NVARCHAR|2|

     ![执行 SQL 任务编辑器 - 参数映射](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-04.jpg "执行 SQL 任务编辑器 - 参数映射")

15. 单击 **"确定"** 以关闭 "**执行 SQL 编辑器**" 对话框。

## <a name="next-step"></a>下一步
 [任务 15：生成和运行 SSIS 项目](../../2014/tutorials/task-15-building-and-running-the-ssis-project.md)


