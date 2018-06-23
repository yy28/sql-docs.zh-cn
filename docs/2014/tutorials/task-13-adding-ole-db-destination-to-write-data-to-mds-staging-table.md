---
title: 任务 13： 添加 OLE DB 目标将数据写入 MDS 临时表 |Microsoft 文档
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
ms.assetid: e6c67fa9-bb52-44a9-82f6-d86551cf12b2
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 75e77579857852e607b783534d149367a946318f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017847"
---
# <a name="task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table"></a>任务 13：添加 OLE DB 目标以便将数据写入 MDS 临时表
  现在，已添加**ImportType**和**BatchTag**所有记录的值，你就可以将其发送转移给 MDS 用于过渡。 在此任务中，你使用 OLE DB 目标将数据写入到**stg.supplier_Leaf**临时表。  
  
1.  拖动**OLE DB 目标**从**其他目标**主题中**SSIS 工具箱**到**数据流**选项卡上，并将其放在**添加列所需的 MDS**。  
  
2.  右键单击**OLE DB 目标**中**数据流**卡，然后单击**重命名**。 类型**将供应商数据写入到 MDS 临时表**按**ENTER**。  
  
3.  连接**添加列所需的 MDS**到**将供应商数据写入到 MDS 临时表**使用蓝色的连接器。  
  
4.  双击**将供应商数据写入到 MDS 临时表**中**数据流**选项卡。  
  
5.  在**OLE DB 目标编辑器**对话框框中，请确保 **（本地）。MDS** (或**localhost。MDS**) 为选择**OLE DB 连接管理器**字段。  
  
6.  选择**stg.Supplier_Leaf**从列表中的表**的表或视图名称**。  
  
     ![OLEDB 目标编辑器](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-01.jpg "OLEDB 目标编辑器")  
  
7.  切换到**映射**页上通过单击**映射**左侧菜单上。  
  
8.  映射**输入**和**目标**列下表中所示。  
  
     ![OLEDB 目标编辑器-映射](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-02.jpg "OLEDB 目标编辑器-映射")  
  
9. 确认你正在使用 **_Output**输入列的列不 **_Status**或 **_Source**列。 **_Output**列包含 DQS 清理的输出值。  
  
10. 单击**确定**关闭**OLE DB 目标编辑器**对话框。  
  
11. 数据流应如下图所示。  
  
     ![完成数据流](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-03.jpg "完成数据流")  
  
## <a name="next-step"></a>下一步  
 [任务 14：将执行 SQL 任务添加到控制流以运行 MDS 的存储过程](../../2014/tutorials/task-14-add-execute-to-control-flow-run-mds-stored-procedure.md)  
  
  