---
title: 创建多维数据集使用多维数据集向导 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d682ada2175d94f7b077bfe06626885862d45e21
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34021994"
---
# <a name="create-a-cube-using-the-cube-wizard"></a>使用多维数据集向导创建多维数据集
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中的多维数据集向导来创建新的多维数据集。  
  
### <a name="to-create-a-new-cube"></a>创建新的多维数据集  
  
1.  在“解决方案资源管理器”中，右键单击“多维数据集”，然后单击“新建多维数据集”。  
  
2.  在多维数据集向导的 **“选择创建方法”** 页上，选择 **“使用现有表”**，然后单击 **“下一步”**。  
  
    > [!NOTE]  
    >  有时可能必须在不使用现有表的情况下创建多维数据集。 若要创建一个空的多维数据集，请选择 **“创建空的多维数据集”**。 若要生成表，请选择 **“在数据源中生成表”**。  
  
3.  在 **“选择度量值组表”** 页上，执行以下操作：  
  
    1.  在 **“数据源视图”** 列表中，选择数据源视图。  
  
    2.  在 **“度量值组表”** 列表中，选择将用于创建度量值组的表。  
  
    3.  单击“下一步” 。  
  
4.  在 **“选择度量值”** 页上，选择要在多维数据集中包含的度量值，然后单击 **“下一步”**。  
  
     另外，您可以更改度量值和度量值组的名称。  
  
5.  在 **“选择现有维度”** 页上，选择要在多维数据集中包含的现有维度，然后单击 **“下一步”**。  
  
    > [!NOTE]  
    >  对于任何选定的度量值组，如果数据库中已存在维度，则会出现“选择现有维度”页。  
  
6.  在 **“选择新维度”** 页上，选择要创建的新维度，然后单击 **“下一步”**。  
  
    > [!NOTE]  
    >  如果有任何表适用于维度表，并且这些表尚未被现有维度使用，则会出现“选择新维度”页。  
  
7.  在 **“选择缺少的维度键”** 页上，为维度选择一个键，然后单击 **“下一步”**。  
  
    > [!NOTE]  
    >  如果指定的任何维度表都未定义键，则会出现“选择缺少的维度键”页。  
  
8.  在 **“完成向导”** 页中，输入新多维数据集的名称，并查看该多维数据集的结构。 若要进行更改，请单击 **“上一步”**；否则，单击 **“完成”**。  
  
    > [!NOTE]  
    >  完成多维数据集向导后，可以使用多维数据集设计器来配置多维数据集。 还可以使用维度设计器来添加、删除和配置所创建维度中的属性和层次结构。  
  
  
