---
title: 从多维数据源导入（SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 7f0793ea-a4c7-42e9-b722-2164a454ebca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 666b7fdf5af10b6726a1e1d7a2aaafa075bf8777
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66080557"
---
# <a name="import-from-a-multidimensional-data-source-ssas-tabular"></a>从多维数据源导入（SSAS 表格）
  可以使用 Analysis Services 多维数据集数据库作为表格模型的数据源。 为了从 Analysis Services 多维数据集导入数据，必须定义一个 MDX 查询以选择要导入的数据。  
  
 SQL Server Analysis Services 数据库包含的任意数据都可以导入到模型。 可以提取维度的全部或一部分，也可以从多维数据集中获取切片和聚合，如当年的销售额总和（逐月列出）等。但是，应记住从多维数据集导入的所有数据都是平展的。 因此，如果定义一个查询针对多个维度检索度量值，则在数据导入时，每个维度将单独占用一列。  
  
 Analysis Services 多维数据集版本必须是 SQL Server 2005、SQL Server 2008、SQL Server 2008 R2、 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]或 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]。  
  
### <a name="to-import-data-from-an-analysis-services-cube"></a>从 Analysis Services 多维数据集导入数据  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，单击 **“模型”** 菜单，然后单击 **“从数据源导入”**。  
  
2.  在 **“连接到数据源”** 页中，选择 **Microsoft Analysis Services**，然后单击 **“下一步”**。  
  
3.  执行表导入向导中的步骤。 可以在 **“指定 MDX 查询”** 页上指定 MDX 查询。 若要使用 MDX 查询设计器，请在“指定 MDX 查询”页上单击 **“设计”**。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSAS 表格&#41;导入数据](import-data-ssas-tabular.md)   
 [&#40;SSAS 表格&#41;支持的数据源](tabular-models/data-sources-supported-ssas-tabular.md)  
  
  
