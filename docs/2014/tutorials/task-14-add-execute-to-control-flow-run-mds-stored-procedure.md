---
title: 任务 14：添加执行 SQL 任务添加到控制流以运行 MDS 的存储的过程 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 9a5d1b52-d505-4e6f-8a89-569329c094e2
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: cf0a02e973d046f3dff2b2df95327cf38e88443c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63222741"
---
# <a name="task-14-adding-execute-sql-task-to-control-flow-to-run-the-stored-procedure-for-mds"></a>任务 14：将执行 SQL 任务添加到控制流以运行 MDS 的存储过程
  在将数据加载到 MDS 的临时表后，您运行与该表相关联的存储过程以便将数据从临时表加载到 MDS 数据库的相应表中。 此存储的过程具有两个需要传递的必需的参数：LogFlag 和 VersionName。 LogFlag 指定在临时过程中是否将事务记入日志，而 VersionName 表示模型版本。 请参阅[临时存储过程](https://msdn.microsoft.com/library/hh231028.aspx)主题的更多详细信息。  
  
 在本任务中，您将执行 SQL 任务添加到控制流中，以便调用该存储过程来将临时数据加载到相应 MDS 表中。  
  
1.  现在，切换到**控制流**选项卡。  
  
2.  拖放**执行 SQL 任务**从**SSIS 工具箱**到**控制流**选项卡。  
  
3.  右键单击**执行 SQL 任务**中**控制流**选项卡，然后单击**重命名**。 类型**触发存储过程以便将数据加载到 MDS**然后按**ENTER**。  
  
4.  连接**接收、 清理、 匹配和组织供应商数据**到**触发存储过程以便将数据加载**使用绿色连接线。  
  
     ![连接到执行 SQL 任务](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-01.jpg "连接以执行 SQL 任务")  
  
5.  使用**变量**窗口中，使用以下设置添加两个新变量。 如果没有看到**变量**窗口中，单击**SSIS**单击菜单栏上**变量**。  
  
    |“属性”|数据类型|ReplTest1|  
    |----------|---------------|-----------|  
    |LogFlag|Int32|1|  
    |VersionName|String|VERSION_1|  
  
     ![SSIS 变量窗口](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-02.jpg "SSIS 变量窗口")  
  
6.  双击**触发存储的过程将数据加载到 MDS**。  
  
7.  在中**执行 SQL 任务编辑器**对话框中，选择 **（本地）。MDS** (或**localhost。MDS**) 用于**连接**。  
  
8.  类型**EXEC [stg]。 [udp_Supplier_Leaf]？，？，？** 有关**SQL 语句**。 您可以使用 SQL Server Management Studio 确认该名称。  
  
     ![执行常规设置的 SQL 编辑器对话框-](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-03.jpg "执行 SQL 编辑器对话框-常规设置")  
  
9. 单击**参数映射**从左侧菜单上。  
  
10. 在中**参数映射**页上，单击**添加**添加映射。 最大化该窗口并且调整列大小，以便您可以正确在下拉列表中看到值。  
  
11. 选择**user:: versionname**从下拉列表中为**变量名称**。  
  
12. 选择**NVARCHAR**有关**数据类型**。  
  
13. 类型**0** （零）**参数名称**。  
  
14. 重复执行前四个步骤以便再添加两个变量。  
  
    |“变量名称”|数据类型（重要）|参数名称|  
    |-------------------|-----------------------------|--------------------|  
    |User::LogFlag|LONG|1|  
    |User::BatchTag|NVARCHAR|2|  
  
     ![执行 SQL 任务编辑器-参数映射](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-04.jpg "执行 SQL 任务编辑器-参数映射")  
  
15. 单击**确定**以关闭**执行 SQL 编辑器**对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 15:生成和运行 SSIS 项目](../../2014/tutorials/task-15-building-and-running-the-ssis-project.md)  
  
  
