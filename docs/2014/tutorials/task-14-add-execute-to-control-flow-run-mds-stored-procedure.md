---
title: 任务 14： 添加执行 SQL 任务，以控制流为 MDS 运行存储的过程 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9a5d1b52-d505-4e6f-8a89-569329c094e2
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 3d364f3e0a2fbff167336bffa6ea5092d0954d14
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017659"
---
# <a name="task-14-adding-execute-sql-task-to-control-flow-to-run-the-stored-procedure-for-mds"></a>任务 14：将执行 SQL 任务添加到控制流以运行 MDS 的存储过程
  在将数据加载到 MDS 的临时表后，您运行与该表相关联的存储过程以便将数据从临时表加载到 MDS 数据库的相应表中。 此存储过程有两个需要传递的必需参数：LogFlag 和 VersionName。 LogFlag 指定在临时过程中是否将事务记入日志，而 VersionName 表示模型版本。 请参阅[暂存存储过程](http://msdn.microsoft.com/library/hh231028.aspx)更多详细信息的主题。  
  
 在本任务中，您将执行 SQL 任务添加到控制流中，以便调用该存储过程来将临时数据加载到相应 MDS 表中。  
  
1.  现在，切换到**控制流**选项卡。  
  
2.  拖放**执行 SQL 任务**从**SSIS 工具箱**到**控制流**选项卡。  
  
3.  右键单击**执行 SQL 任务**中**控制流**卡，然后单击**重命名**。 类型**触发器将数据加载到 MDS 存储过程**按**ENTER**。  
  
4.  连接**接收、 清理、 匹配项，而 Curate 供应商数据**到**触发器到加载数据的存储过程**使用绿色的连接器。  
  
     ![连接到执行 SQL 任务](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-01.jpg "连接到执行 SQL 任务")  
  
5.  使用**变量**窗口中，添加具有以下设置的两个新变量。 如果看不到**变量**窗口中，单击**SSIS**单击菜单栏上**变量**。  
  
    |“属性”|数据类型|ReplTest1|  
    |----------|---------------|-----------|  
    |LogFlag|Int32|@shouldalert|  
    |VersionName|String|VERSION_1|  
  
     ![SSIS 变量窗口](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-02.jpg "SSIS 变量窗口")  
  
6.  双击**触发存储的过程以将数据加载到 MDS**。  
  
7.  在**执行 SQL 任务编辑器**对话框中，选择 **（本地）。MDS** (或**localhost。MDS**) 为**连接**。  
  
8.  类型**EXEC [stg]。 [udp_Supplier_Leaf]？，？，？** 有关**SQL 语句**。 您可以使用 SQL Server Management Studio 确认该名称。  
  
     ![执行 SQL 编辑器对话框中的常规设置](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-03.jpg "' 执行 SQL 编辑器对话框-常规设置")  
  
9. 单击**参数映射**从左侧菜单。  
  
10. 在**参数映射**页上，单击**添加**若要添加的映射。 最大化该窗口并且调整列大小，以便您可以正确在下拉列表中看到值。  
  
11. 选择**User::VersionName**从下拉列表中为**变量名称**。  
  
12. 选择**NVARCHAR**为**数据类型**。  
  
13. 类型**0** （零）**参数名称**。  
  
14. 重复执行前四个步骤以便再添加两个变量。  
  
    |“变量名称”|数据类型（重要）|参数名称|  
    |-------------------|-----------------------------|--------------------|  
    |User::LogFlag|LONG|@shouldalert|  
    |User::BatchTag|NVARCHAR|2|  
  
     ![执行 SQL 任务编辑器的参数映射](../../2014/tutorials/media/et-addingesqltasktocftorunthespformds-04.jpg "执行 SQL 任务编辑器的参数映射")  
  
15. 单击**确定**关闭**执行 SQL 编辑器**对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 15：生成和运行 SSIS 项目](../../2014/tutorials/task-15-building-and-running-the-ssis-project.md)  
  
  