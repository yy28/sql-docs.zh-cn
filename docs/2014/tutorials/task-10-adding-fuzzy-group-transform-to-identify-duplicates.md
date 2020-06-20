---
title: 任务10：添加模糊分组转换以确定重复项 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 90b2b323-babd-464a-8914-9dc5e66aca74
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e7091c4dbb8244476357afba18e973535def8baa
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064806"
---
# <a name="task-10-adding-fuzzy-group-transform-to-identify-duplicates"></a>任务 10：添加模糊分组转换以确定重复项
  在本任务中，您向数据流添加模糊分组转换。 模糊分组转换可有助于标识源数据中的重复项。 有关更多详细信息，请参阅[模糊分组转换](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)。  
  
1.  将 " **SSIS 工具箱**" 中**其他转换**中的 "**模糊组**转换" 拖放到 **"数据流" 选项卡**下的 "**合并正确和已更正的记录**"。  
  
2.  右键单击 **"数据流" 选项卡**中的 "**模糊组**转换"，然后单击 "**重命名**"。 键入**组具有匹配 id 的供应商**，然后按**enter**。  
  
3.  连接结合使用蓝色连接器将**正确和更正的记录合并**到**具有匹配 Id 的组供应商**。  
  
     ![连接到具有匹配 ID 的组供应商](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-01.jpg "连接到具有匹配 ID 的组供应商")  
  
4.  双击 "**组具有匹配 id 的供应商**"。  
  
5.  在 "**模糊分组转换编辑器**" 中，单击 " **OLE DB 连接管理器" 下拉列表**旁边的 "**新建**" 以启动 "**配置 OLE DB 连接管理器**" 对话框。  
  
6.  在对话框中，单击 "**新建**" 以启动 "**连接管理器**" 对话框。  
  
7.  键入 **（local）** 或**句点**（.）作为服务器名称。  
  
8.  选择 " **MDS** "，**选择或输入数据库名称**字段。 将使用 MDS 数据库作为**模糊组转换**的临时存储。 **模糊分组**转换要求与 SQL Server 的实例建立连接，以创建转换算法完成其工作所需的临时 SQL Server 表。 您可以为此目的创建一个数据库或使用其他现有数据库。  
  
9. 单击 "**测试连接**" 以测试连接，然后在消息框上单击 **"确定"** 。  
  
10. 在 "**连接管理器**" 对话框中，单击 **"确定"**。  
  
11. 选择 " **（本地）"。MDS** （或**localhost。MDS**） **，然后单击** **"确定"**。  
  
12. 在 "**模糊分组转换编辑器**" 中，确认 " **（local）"。MDS**或**localhost。** 选择了 MDS 作为**OLE DB 连接管理器**。  
  
13. 切换到 "**列**" 选项卡。  
  
14. 从**可用输入列**的列表中选择（复选框） **SupplierID_Output** 。 为了配置该转换，请选择在标识重复项时要使用的输入列。 为简单易懂，您在此步骤中仅使用 SupplierID。  
  
     ![模糊分组转换编辑器](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-02.jpg "模糊分组转换编辑器")  
  
15. 单击 **"确定"** 以关闭 "**模糊组转换编辑器**"。  
  
## <a name="next-step"></a>下一步  
 [任务 11：添加有条件拆分转换以筛选重复项](../../2014/tutorials/task-11-adding-conditional-split-transform-to-filter-duplicates.md)  
  
  
