---
title: 任务 13:添加 OLE DB 目标将数据写入 MDS 临时表 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e6c67fa9-bb52-44a9-82f6-d86551cf12b2
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 34f68c4604d70dc83579f8c9284802b82cc6291d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56035068"
---
# <a name="task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table"></a>任务 13:添加 OLE DB 目标以便将数据写入 MDS 临时表
  现在，已添加**ImportType**并**BatchTag**所有记录的值，现在可以将它们发送到 MDS 的过渡环境。 在本任务中，使用 OLE DB 目标将数据写入**stg.supplier_Leaf**临时表。  
  
1.  拖动**OLE DB Destination**从**其他目标**主题中**SSIS 工具箱**到**数据流**选项卡并将其放置在**添加 MDS 所需的列**。  
  
2.  右键单击**OLE DB Destination**中**数据流**选项卡，然后单击**重命名**。 类型**供应商数据写入 MDS 临时表**然后按**ENTER**。  
  
3.  连接**添加列所需的 MDS**到**供应商数据写入 MDS 临时表**使用蓝色连接器。  
  
4.  双击**供应商数据写入 MDS 临时表**中**数据流**选项卡。  
  
5.  在中**OLE DB 目标编辑器**对话框框中，请确保 **（本地）。MDS** (或**localhost。MDS**) 为所选**OLE DB 连接管理器**字段。  
  
6.  选择**stg.Supplier_Leaf**从列表中的表**的表或视图名称**。  
  
     ![OLEDB 目标编辑器](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-01.jpg "OLEDB 目标编辑器")  
  
7.  切换到**映射**通过单击页面**映射**左侧菜单上。  
  
8.  地图**输入**并**目标**列下表中所示。  
  
     ![OLEDB 目标编辑器-映射](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-02.jpg "OLEDB 目标编辑器-映射")  
  
9. 确认您使用的 **_Output**输入列的列不 **_Status**或 **_Source**列。 **_Output**列包含来自 DQS 清理的输出值。  
  
10. 单击**确定**以关闭**OLE DB 目标编辑器**对话框。  
  
11. 数据流应如下图所示。  
  
     ![完成数据流](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-03.jpg "完成数据流")  
  
## <a name="next-step"></a>下一步  
 [任务 14:添加执行 SQL 任务添加到控制流以运行 MDS 的存储的过程](../../2014/tutorials/task-14-add-execute-to-control-flow-run-mds-stored-procedure.md)  
  
  
