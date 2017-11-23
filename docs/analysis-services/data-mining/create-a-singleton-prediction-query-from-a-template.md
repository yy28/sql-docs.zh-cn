---
title: "从模板创建单独预测查询 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: singleton query predictions [DMX]
ms.assetid: e0a68ab0-bece-4d25-b464-47f1719302e6
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7b455a9f4c8996ec2dd9e6d255f4e9f282d58df4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="create-a-singleton-prediction-query-from-a-template"></a>通过模板创建单独预测查询
  如果您具有一个要用于预测的模型，但不希望将该模型映射到外部输入数据集或生成大容量预测，则单独查询很有用。 对于单独查询，您可以向模型提供一个或多个值，并且立即会看到预测值。  
  
 例如，以下 DMX 查询表示对目标邮件模型 TM_Decision_Tree 的单独查询。  
  
```  
SELECT * FROM [TM_Decision_tree] ;  
NATURAL PREDICTION JOIN  
(SELECT '2' AS [Number Children At Home], '45' as [Age])  
AS [t]  
```  
  
 其后的过程介绍如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的模板资源管理器来快速创建此查询。  
  
### <a name="to-open-the-analysis-services-templates-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中打开 Analysis Services 模板  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的 **“视图”** 菜单上，单击 **模板资源管理器**。  
  
2.  单击多维数据集图标以打开 **Analysis Server**模板。  
  
### <a name="to-open-a-prediction-query-template"></a>打开预测查询模板  
  
1.  在“模板资源管理器”的“Analysis Server”模板列表中，依次展开“DMX”和“预测查询”。  
  
2.  双击“单独预测”。  
  
3.  在 **“连接到 Analysis Services”** 对话框中，键入服务器的名称，该服务器具有包含要查询的挖掘模型的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例。  
  
4.  单击 **“连接”**。  
  
5.  模板在指定的数据库中打开，同时打开的还有挖掘模型对象浏览器，其中包含数据挖掘函数和数据挖掘结构以及相关模型的列表。  
  
### <a name="to-customize-the-singleton-query-template"></a>自定义单独查询模板  
  
1.  在模板中，单击“可用数据库”下拉列表，然后从列表中选择一个 Analysis Service 实例。  
  
2.  在 **“挖掘模型”** 列表中，选择您要查询的挖掘模型。  
  
     挖掘模型中的列的列表显示在对象浏览器的 **“元数据”** 窗格中。  
  
3.  在 **“查询”** 菜单上，选择 **“指定模板参数的值”**。  
  
4.  在“选择列表”行，键入 * 以返回所有列，或键入以逗号分隔的列和表达式的列表以返回特定的列。  
  
     如果您键入 *，则会返回可预测列以及您在步骤 6 中为其提供新值的任何列。  
  
     对于本主题开头部分显示的示例代码，“选择列表”行设置为 *。  
  
5.  在 **“挖掘模型”** 行，键入显示在 **“对象资源管理器”**中的挖掘模型列表中的挖掘模型的名称。  
  
     对于本主题开头部分显示的示例代码，“挖掘模型”行设置为名称 **TM_Decision_Tree**。  
  
6.  在 **“值”** 行中，键入您要对其进行预测的新数据值。  
  
     对于本主题开头部分显示的示例代码，  “值”行设置为 **2** 以根据家庭子女数预测自行车购买行为。  
  
7.  在 **“列”** 行中，键入新数据映射到的挖掘模型中列的名称。  
  
     对于本主题开头部分显示的示例代码，  “列”行设置为 **Number Children at Home**。  
  
    > [!NOTE]  
    >  使用 **“指定模板参数的值”** 对话框时，不必将列名称用方括号括起来。 括号会自动添加。  
  
8.  将  “输入别名”保留为 **t**。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. 在查询文本窗格中，查找指示语法错误的逗号和省略号下的红色波形曲线。 删除省略号，并添加任何其他想要的查询条件。 如果不需要添加任何其他条件，请删除逗号。  
  
     对于本主题开头部分显示的示例代码，其他查询条件设置为 **'45' as [Age]**。  
  
11. 单击 **“执行”**。  
  
## <a name="see-also"></a>另请参阅  
 [创建预测（数据挖掘基础教程）](http://msdn.microsoft.com/library/a8410ed2-bb98-4d51-a9eb-b239be1201c2)  
  
  
