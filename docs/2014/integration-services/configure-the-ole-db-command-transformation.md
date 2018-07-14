---
title: 配置 OLE DB 命令转换 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- parameters [Integration Services]
- OLE DB Command transformation
ms.assetid: c800f167-3d2e-4c10-8ba3-a02f1872ccea
caps.latest.revision: 24
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a29642a667d4d22ecf5c7f6d3de0848b4725df91
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37254479"
---
# <a name="configure-the-ole-db-command-transformation"></a>配置 OLE DB 命令转换
  若要添加和配置 OLE DB 命令转换，包必须已包含至少一个数据流任务和一个源（如平面文件源或 OLE DB 源）。 这种转换通常用于运行参数化查询。  
  
### <a name="to-configure-the-ole-db-command-transformation"></a>配置 OLE DB 命令转换  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“数据流”** 选项卡，然后从 **“工具箱”** 中将 OLE DB 命令转换拖动到设计图面。  
  
4.  将连接线（绿色或红色箭头）从数据源或前一个转换拖动到 OLE DB 命令转换，从而将 OLE DB 命令转换连接到数据流。  
  
5.  右键单击组件，并选择“编辑高级编辑器”或“显示高级编辑器”。  
  
6.  在 **“连接管理器”** 选项卡上，从 **“连接管理器”** 列表中选择 OLE DB 连接管理器。 有关详细信息，请参阅 [OLE DB Connection Manager](connection-manager/ole-db-connection-manager.md)。  
  
7.  单击“组件属性”选项卡，并单击 **SqlCommand** 框中的省略号按钮 **(…)**。  
  
8.  在“字符串值编辑器”中，键入参数化 SQL 语句，并且使用问号 (?) 作为每个参数的参数标记。  
  
9. 单击 **“刷新”**。 单击“刷新”时，转换将为 External Columns 集合中的每一个参数都创建一列，并设置 DBParamInfoFlags 属性。  
  
10. 单击 **“输入属性和输出属性”** 选项卡。  
  
11. 展开 **“OLE DB 命令输入”**，再展开 **“外部列”**。  
  
12. 验证 **“外部列”** 是否为 SQL 语句中的每个参数列出了一列。 列的名称是 **Param_0**、 **Param_1**，以此类推。  
  
     不应更改列名称。 如果更改列名称， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 会生成有关 OLE DB 命令转换的验证错误。  
  
     此外，不应更改数据类型。 每列的 DataType 属性均设置为正确的数据类型。  
  
13. 如果 **“外部列”** 没有列出任何列，则您必须手动添加这些列。  
  
    -   对 SQL 语句中的每一个参数，单击一次 **“添加列”** 。  
  
    -   将列名更新为 **Param_0**、 **Param_1**，以此类推。  
  
    -   在 DBParamInfoFlags 属性中指定值。 该值必须与 OLE DB DBPARAMFLAGSENUM 枚举中的值相匹配。 有关详细信息，请参阅 OLE DB 参考文档。  
  
    -   指定列的数据类型，并根据该数据类型指定列的代码页、长度、精度和小数位数。  
  
    -   若要删除未使用的参数，请选择 **“外部列”** 中的参数，再单击 **“删除列”**。  
  
    -   单击 **“列映射”** ，并将 **“可用输入列”** 列表中的列映射到 **“可用目标列”** 列表中的参数。  
  
14. 单击“确定” 。  
  
15. 若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存”** 。  
  
## <a name="see-also"></a>请参阅  
 [OLE DB 命令转换](data-flow/transformations/ole-db-command-transformation.md)   
 [Integration Services 转换](data-flow/transformations/integration-services-transformations.md)   
 [Integration Services 路径](data-flow/integration-services-paths.md)   
 [数据流任务](control-flow/data-flow-task.md)  
  
  
