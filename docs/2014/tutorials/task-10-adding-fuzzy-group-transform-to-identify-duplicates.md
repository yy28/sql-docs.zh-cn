---
title: 任务 10： 添加模糊分组转换来标识重复 |Microsoft 文档
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
ms.assetid: 90b2b323-babd-464a-8914-9dc5e66aca74
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: cf9ad3dff4737d7308e7ec3434985b18015f29d8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026916"
---
# <a name="task-10-adding-fuzzy-group-transform-to-identify-duplicates"></a>任务 10：添加模糊分组转换以确定重复项
  在本任务中，您向数据流添加模糊分组转换。 模糊分组转换可有助于标识源数据中的重复项。 请参阅[模糊分组转换](http://msdn.microsoft.com/library/ms141764.aspx)有关详细信息。  
  
1.  拖放**Fuzzy 组**在中转换**其他转换**上**SSIS 工具箱**到**数据流**下**合并的正确和更正记录**。  
  
2.  右键单击**Fuzzy 组**在中转换**数据流**卡，然后单击**重命名**。 类型**组具有匹配 Id 的供应商**按**ENTER**。  
  
3.  连接**正确合并和更正的记录**到**组具有匹配 Id 的供应商**使用蓝色的连接器。  
  
     ![连接到具有匹配 Id 的组供应商](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-01.jpg "到具有匹配 Id 的组供应商的连接")  
  
4.  双击**组具有匹配 Id 的供应商**。  
  
5.  在**模糊组转换编辑器**，单击**新建**旁边**OLE DB 连接管理器下拉列表**以启动**配置 OLE DB 连接Manager**对话框。  
  
6.  在对话框中，单击**新建**以启动**连接管理器**对话框。  
  
7.  类型 **（本地）** 或**段**（.） 的服务器名称。  
  
8.  选择**MDS**为**选择或输入数据库名称**字段。 将 MDS 数据库的临时存储用作**模糊组转换**。 **模糊分组**转换要求连接到要创建的临时的 SQL Server 表，该转换算法完成其工作所需的 SQL Server 实例。 您可以为此目的创建一个数据库或使用其他现有数据库。  
  
9. 单击**测试连接**以测试连接，并单击**确定**消息框上。  
  
10. 在**连接管理器**对话框中，单击**确定**。  
  
11. 选择 **（本地）。MDS** (或**localhost。MDS**) 从**列表的数据连接**单击**确定**。  
  
12. 在**模糊分组转换编辑器**，确认 **（本地）。MDS**或**localhost。MDS**为选择**OLE DB 连接管理器**。  
  
13. 切换到**列**选项卡。  
  
14. 选择 （复选框） **SupplierID_Output**从列表中**可用输入列**。 为了配置该转换，请选择在标识重复项时要使用的输入列。 为简单易懂，您在此步骤中仅使用 SupplierID。  
  
     ![模糊分组转换编辑器](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-02.jpg "模糊分组转换编辑器")  
  
15. 单击**确定**关闭**模糊组转换编辑器**。  
  
## <a name="next-step"></a>下一步  
 [任务 11：添加有条件拆分转换以筛选重复项](../../2014/tutorials/task-11-adding-conditional-split-transform-to-filter-duplicates.md)  
  
  