---
title: 点击链接型报表 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- clickthrough reports
- customizing clickthrough reports
- clickthrough reports, customizing
ms.assetid: cf2c396e-b0c6-41f9-8c45-ddc8406f7e85
caps.latest.revision: 28
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: c6bb00e29b5edc039d33a345addc596f18669f3e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129604"
---
# <a name="clickthrough-reports-ssrs"></a>点击链接型报表 (SSRS)
  点击链接型报表是一种用于提供有关主报表数据的详细信息的报表。 当用户单击主报表中显示的交互式数据时，便会显示点击链接型报表。 这些报表是由报表服务器自动生成的。 你，模型设计器中，应确定中显示的内容点击链接型报表通过设置`DefaultDetailAttribute`和`DefaultAggregateAttribute`分配到报表模型中实体的属性。  
  
> [!NOTE]  
>  点击链接型报表不可用的每个版本[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 有关支持的版本的功能的列表[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，请参阅[支持的 SQL Server 2014 的版本功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。 如果不能确定您的单位所运行的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的版本，请与数据库管理员联系。  
  
## <a name="using-default-templates"></a>使用默认模板  
 默认情况下，报表服务器针对每个实体生成两种点击链接型模板类型：单个实例模板和多个实例模板。 使用哪类模板取决于您所单击的项。 如果读取报表的人员单击标量属性，则使用单个实例模板。 如果读取报表的人员单击聚合属性，则使用多个实例模板。  
  
#### <a name="single-instance-templates"></a>单个实例模板  
 单个实例模板显示目标实体的所有属性以及为与目标实体有一对多关系的相关实体指定的所有默认聚合特性。 单个实例模板的外观与下图类似。  
  
 ![多对一点击链接型报表。](../media/manytooneclickthrough.gif "A many to 1 clickthrough report.")  
  
#### <a name="multiple-instance-templates"></a>多个实例模板  
 多个实例模板只显示目标实体的默认详细信息属性，以及为与目标实体有一对多关系的相关实体指定的所有默认聚合特性。 多个实例模板的外观与下图类似。  
  
 ![多对一点击链接型报表。](../media/onetomanyclickthrough.gif "A many to 1 clickthrough report.")  
  
## <a name="customizing-clickthrough-reports"></a>自定义点击链接型报表  
 您可以不使用报表服务器生成的默认模板，而是在报表生成器中创建报表并将其用作自定义点击链接型报表。 然后，便可以在报表管理器中将您的报表作为钻取报表链接到模型。  
  
 若要将报表生成器报表转换为点击链接型报表，需要在报表生成器的 **“属性”** 对话框中选择 **“允许钻取到此报表”** 选项。 选中该选项后，便会向报表中添加一个钻取参数，并且报表无法再在报表生成器中直接运行。 当读取报表的人员单击报表生成器报表中的某项时，报表服务器将自动计算钻取参数。  
  
> [!IMPORTANT]  
>  报表中使用的主实体（或基实体）必须与报表所链接到的实体相同。  
  
## <a name="see-also"></a>请参阅  
 [将报表作为点击链接型报表链接到模型](../link-a-report-to-a-model-as-a-clickthrough-report.md)  
  
  