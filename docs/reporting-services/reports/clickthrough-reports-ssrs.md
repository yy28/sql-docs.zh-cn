---
title: "点击链接型报表 (SSRS) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clickthrough reports
- customizing clickthrough reports
- clickthrough reports, customizing
ms.assetid: cf2c396e-b0c6-41f9-8c45-ddc8406f7e85
caps.latest.revision: 28
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 55d22d2fd64faef6e913bf226c831546d71665ca
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="clickthrough-reports-ssrs"></a>点击链接型报表 (SSRS)
  点击链接型报表是一种用于提供有关主报表数据的详细信息的报表。 当用户单击主报表中显示的交互式数据时，便会显示点击链接型报表。 这些报表是由报表服务器自动生成的。 作为模型设计者，您可以通过在报表模型中设置分配给某实体的 **DefaultDetailAttribute** 和 **DefaultAggregateAttribute** 属性来确定点击链接型报表中显示的内容。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个版本中均不提供点击链接型报表。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。 如果不能确定您的单位所运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本，请与数据库管理员联系。  
  
## <a name="using-default-templates"></a>使用默认模板  
 默认情况下，报表服务器针对每个实体生成两种点击链接型模板类型：单个实例模板和多个实例模板。 使用哪类模板取决于您所单击的项。 如果读取报表的人员单击标量属性，则使用单个实例模板。 如果读取报表的人员单击聚合属性，则使用多个实例模板。  
  
#### <a name="single-instance-templates"></a>单个实例模板  
 单个实例模板显示目标实体的所有属性以及为与目标实体有一对多关系的相关实体指定的所有默认聚合特性。 单个实例模板的外观与下图类似。  
  
 ![多对 1 的点击链接型报表。](../../reporting-services/reports/media/manytooneclickthrough.gif "多对 1 的点击链接型报表。")  
  
#### <a name="multiple-instance-templates"></a>多个实例模板  
 多个实例模板只显示目标实体的默认详细信息属性，以及为与目标实体有一对多关系的相关实体指定的所有默认聚合特性。 多个实例模板的外观与下图类似。  
  
 ![多对 1 的点击链接型报表。](../../reporting-services/reports/media/onetomanyclickthrough.gif "多对 1 的点击链接型报表。")  
  
## <a name="customizing-clickthrough-reports"></a>自定义点击链接型报表  
 您可以不使用报表服务器生成的默认模板，而是在报表生成器中创建报表并将其用作自定义点击链接型报表。 然后，便可以在报表管理器中将您的报表作为钻取报表链接到模型。  
  
 若要将报表生成器报表转换为点击链接型报表，需要在报表生成器的 **“属性”** 对话框中选择 **“允许钻取到此报表”** 选项。 选中该选项后，便会向报表中添加一个钻取参数，并且报表无法再在报表生成器中直接运行。 当读取报表的人员单击报表生成器报表中的某项时，报表服务器将自动计算钻取参数。  
  
> [!IMPORTANT]  
>  报表中使用的主实体（或基实体）必须与报表所链接到的实体相同。  
  
## <a name="see-also"></a>另请参阅  
 [将报表作为点击链接型报表链接到模型](http://msdn.microsoft.com/library/3af42de3-67ef-41c2-bc8a-7045baec6f63)  
  
  

