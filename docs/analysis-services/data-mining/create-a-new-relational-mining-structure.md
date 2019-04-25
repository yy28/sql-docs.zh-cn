---
title: 创建新的关系挖掘结构 |Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e111345276fdf2895b7eb4d056b046efe20b32e9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740507"
---
# <a name="create-a-new-relational-mining-structure"></a>创建新的关系挖掘结构
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  通过数据挖掘向导使用相关数据库或其他源中的数据来创建新的挖掘结构，然后将该结构和任何相关模型保存到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中。  
  
## <a name="to-create-a-relational-mining-structure"></a>创建关系挖掘结构  
  
1.  在解决方案资源管理器中，右键单击 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中的“挖掘结构”文件夹，再单击“新建挖掘结构”。  
  
     此时将打开数据挖掘向导。  
  
2.  在 **“欢迎使用数据挖掘向导”** 页上，单击 **“下一步”**。  
  
3.  在 **“选择定义方法”** 页中，选择 **“从现有关系数据库或数据仓库”**，再单击 **“下一步”**。  
  
4.  在 **“选择数据挖掘技术”** 页中，选择要使用的数据挖掘算法，再单击 **“下一步”**。  
  
     有关数据挖掘算法的详细信息，请参阅[数据挖掘算法（Analysis Services - 数据挖掘）](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)。  
  
5.  在 **“选择数据源视图”** 页中的 **“可用数据源视图”** 下，单击要使用的数据源视图，再单击 **“下一步”**。  
  
     有关创建数据源视图的详细信息，请参阅 [多维模型中的数据源视图](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)。  
  
6.  在 **“指定表类型”** 页中的 **“输入表”** 下，选择一个事例表和一个嵌套表。  
  
7.  在 **“指定定型数据”** 页中的 **“挖掘模型结构”** 下，选择键列、输入列和可预测列。  
  
     选择可预测列后，可以单击 **“建议”** 按钮以打开 **“提供相关列建议”** 对话框。 在该对话框中，单击 **“确定”** 可以接受建议的列，以将所选列包含到挖掘结构中；也可以在 **“输入”** 列中先更改选择的列，再单击 **“确定”**。 若要忽略建议，请单击 **“取消”**。  
  
8.  单击“下一步” 。  
  
9. 在 **“指定列的内容和数据类型”** 页的 **“挖掘模型结构”** 下，可以调整每列的内容类型和数据类型。  
  
    > [!NOTE]  
    >  您可以单击 **“检测”** 以自动检测列包含的是连续数据还是离散数据。 单击该按钮后，系统即会更新 **“内容类型”** 和 **“数据类型”** 两列中的列内容类型和数据类型。 有关内容类型和数据类型的详细信息，请参阅[内容类型（数据挖掘）](../../analysis-services/data-mining/content-types-data-mining.md)和[数据类型（数据挖掘）](../../analysis-services/data-mining/data-types-data-mining.md)。  
  
10. 单击“下一步” 。  
  
11. 在 **“完成向导”** 页中，为将要创建的挖掘结构和相关的初始挖掘模型提供一个名称，再单击 **“完成”**。  
  
## <a name="see-also"></a>请参阅  
 [挖掘结构任务和操作指南](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
