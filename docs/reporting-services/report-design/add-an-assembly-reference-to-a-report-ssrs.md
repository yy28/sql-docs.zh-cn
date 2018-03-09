---
title: "向报表添加程序集引用 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- code [Reporting Services]
- custom assemblies [Reporting Services], referencing
- custom code [Reporting Services]
- adding assembly references
- assemblies [Reporting Services], references
ms.assetid: 0a03939e-48ce-4c30-b227-98533f2e0ccb
caps.latest.revision: "43"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: d9b401410ff01a5e32dcac8ab61e4b5a0bf859d0
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="add-an-assembly-reference-to-a-report-ssrs"></a>向报表添加程序集引用 (SSRS)
  嵌入包含对 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 类的引用的自定义代码时，如果这些类不是 <xref:System.Math> 或 <xref:System.Convert>中的类，则必须提供对报表的程序集引用，以使报表处理器能够解析名称。 有关详细信息，请参阅[向报表添加代码 (SSRS)](../../reporting-services/report-design/add-code-to-a-report-ssrs.md)。  
  
### <a name="to-add-an-assembly-reference-to-a-report"></a>向报表添加程序集引用  
  
1.  在“设计”视图中，右键单击报表边框外的设计图面，然后单击“报表属性”。  
  
2.  单击 **“引用”**。  
  
3.  在 **“添加或删除程序集”**中，单击 **“添加”** ，然后单击省略号按钮浏览到程序集。  
  
4.  在 **“添加或删除类”**中，单击 **“添加”** ，然后键入类的名称，并提供要在报表中使用的实例名。  
  
    > [!NOTE]  
    >  仅为基于实例的成员指定类名称和实例名。 请不要在 **“类”** 列表中指定静态成员。 有关详细信息，请参阅 [报表设计器的表达式中的自定义代码和程序集引用 (SSRS)](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另请参阅  
 [将自定义程序集用于报表](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [“报表属性”对话框 ->“引用”](http://msdn.microsoft.com/library/4639d368-9918-4bb1-9953-7a724ca78dea)  
  
  
