---
title: "向报表添加程序集引用 (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "代码 [Reporting Services]"
  - "自定义程序集 [Reporting Services], 引用"
  - "自定义代码 [Reporting Services]"
  - "添加程序集引用"
  - "程序集 [Reporting Services], 引用"
ms.assetid: 0a03939e-48ce-4c30-b227-98533f2e0ccb
caps.latest.revision: 43
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 43
---
# 向报表添加程序集引用 (SSRS)
  嵌入包含对 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 类的引用的自定义代码时，如果这些类不是 <xref:System.Math> 或 <xref:System.Convert> 中的类，则必须提供对报表的程序集引用，以使报表处理器能够解析名称。 有关详细信息，请参阅[向报表添加代码 (SSRS)](../../reporting-services/report-design/add-code-to-a-report-ssrs.md)。  
  
### 向报表添加程序集引用  
  
1.  在“设计”视图中，右键单击报表边框外的设计图面，然后单击“报表属性”。  
  
2.  单击 **“引用”**。  
  
3.  在 **“添加或删除程序集”**中，单击 **“添加”** ，然后单击省略号按钮浏览到程序集。  
  
4.  在 **“添加或删除类”**中，单击 **“添加”** ，然后键入类的名称，并提供要在报表中使用的实例名。  
  
    > [!NOTE]  
    >  仅为基于实例的成员指定类名称和实例名。 请不要在 **“类”** 列表中指定静态成员。 有关详细信息，请参阅[报表设计器的表达式中的自定义代码和程序集引用 (SSRS)](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## 另请参阅  
 [将自定义程序集用于报表](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [“报表属性”对话框 ->“引用”](../Topic/Report%20Properties%20Dialog%20Box,%20References.md)  
  
  