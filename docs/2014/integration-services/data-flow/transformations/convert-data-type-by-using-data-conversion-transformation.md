---
title: 将数据转换为不同的数据类型，方法是使用数据转换转换 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: 4aabbe4f-7666-4672-865a-9627bd25fbfd
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: bddfd8409bcca80a468638398270c7479e02d62f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015491"
---
# <a name="convert-data-to-a-different-data-type-by-using-the-data-conversion-transformation"></a>使用数据转换将数据转换为其他数据类型
  若要添加并配置数据转换，包必须已经包含至少一个数据流任务和一个源。  
  
### <a name="to-convert-data-to-a-different-data-type"></a>将数据转换为其他数据类型  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中，打开包含所需包的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  单击 **“数据流”** 选项卡，再从 **“工具箱”** 中将数据转换拖动到设计图面。  
  
4.  将连接线从源或前一转换拖到数据转换，从而将数据转换连接到数据流。  
  
5.  双击此数据转换。  
  
6.  在“数据转换编辑器”对话框的“可用输入列”表中，选中位于要转换其数据类型的列旁边的复选框。  
  
    > [!NOTE]  
    >  可以将多个数据转换应用到一个输入列。  
  
7.  也可以在 **“输出别名”** 列中修改默认值。  
  
8.  在 **“数据类型”** 列表中，选择列的新数据类型。 默认数据类型为输入列的数据类型。  
  
9. 也可以根据所选数据类型更新 **“长度”**、 **“精度”**、 **“小数位数”** 和 **“代码页”** 列的值。  
  
10. 若要配置错误输出，请单击 **“配置错误输出”**。 有关详细信息，请参阅 [在数据流组件中配置错误输出](../../configure-an-error-output-in-a-data-flow-component.md)。  
  
11. 单击“确定” 。  
  
12. 若要保存更新后的包，请单击 **“文件”** 菜单上的 **“保存选定项”** 。  
  
## <a name="see-also"></a>请参阅  
 [数据转换](data-conversion-transformation.md)   
 [Integration Services 转换](integration-services-transformations.md)   
 [Integration Services 路径](../integration-services-paths.md)   
 [Integration Services 数据类型](../integration-services-data-types.md)   
 [数据流任务]((../../control-flow/data-flow-task.md)  
  
  