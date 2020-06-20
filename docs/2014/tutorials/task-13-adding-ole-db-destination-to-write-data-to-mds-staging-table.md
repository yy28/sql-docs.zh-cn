---
title: 任务13：添加 OLE DB 目标以便将数据写入 MDS 临时表 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e6c67fa9-bb52-44a9-82f6-d86551cf12b2
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bb39e9d50d135adfedcf307cda2ad703e302eda5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061137"
---
# <a name="task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table"></a>任务 13：添加 OLE DB 目标以便将数据写入 MDS 临时表
  将**ImportType**和**BatchTag**值添加到所有记录后，便可以将它们发送到 MDS 进行过渡。 在此任务中，将使用 OLE DB 目标将数据写入 stg.<name 临时表中**supplier_Leaf。**  
  
1.  将 " **SSIS 工具箱**" 中的 "**其他目标**" **OLE DB "目标**" 拖到 **"数据流" 选项卡**，并将其放在 "**添加 MDS 所需的列**" 下  
  
2.  右键单击 "**数据流**" 选项卡中**OLE DB "目标**"，然后单击 "**重命名**"。 键入 "**将供应商数据写入 MDS 临时表**"，然后按**enter**。  
  
3.  使用蓝色连接器连接**Mds 所需的 "添加列**" 将**供应商数据写入 mds 临时表**。  
  
4.  双击 **"数据流" 选项**卡上的 "**将供应商数据写入 MDS 临时表**"。  
  
5.  在 " **OLE DB 目标编辑器**" 对话框中，确保 " **（local）"。MDS** （或**localhost。MDS**）为**OLE DB 连接管理器**"字段选择。  
  
6.  选择**stg.<name。** 从**表或视图的名称**列表中 Supplier_Leaf 表。  
  
     ![OLEDB 目标编辑器](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-01.jpg "OLEDB 目标编辑器")  
  
7.  单击左侧菜单上的 "**映射**"，切换到 "**映射**" 页。  
  
8.  映射**输入**列和**目标**列，如下表所示。  
  
     ![OLEDB 目标编辑器 - 映射](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-02.jpg "OLEDB 目标编辑器 - 映射")  
  
9. 确认您使用的是输入列 **_Output**列，而不是 **_Status**或 **_Source**列。 **_Output**列包含 DQS 清理中的输出值。  
  
10. 单击 **"确定"** 以关闭 " **OLE DB 目标编辑器**" 对话框。  
  
11. 数据流应如下图所示。  
  
     ![已完成的数据流](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-03.jpg "已完成的数据流")  
  
## <a name="next-step"></a>后续步骤  
 [任务 14：将执行 SQL 任务添加到控制流以运行 MDS 的存储过程](../../2014/tutorials/task-14-add-execute-to-control-flow-run-mds-stored-procedure.md)  
  
  
