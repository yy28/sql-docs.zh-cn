---
title: "查看 Analysis Services 项目的 XML (SSDT) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "项目 [Analysis Services], 查看 XML"
ms.assetid: dd1a4bc6-57b5-47df-8619-09f921aa6351
caps.latest.revision: 14
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 14
---
# 查看 Analysis Services 项目的 XML (SSDT)
  在项目模式下使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库时， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 为项目文件夹中的每个对象创建 XML 定义。 您可以查看 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中每个对象的 XML 文件的内容， 还可以直接编辑 XML 文件；但是，大多数情况下不建议这样做，因为您所做的更改可能会使 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]无法读取 XML。  
  
> [!NOTE]  
>  您无法查看整个项目的 XML 代码，但是可以查看每个对象的代码，因为每个对象都有单独的文件。 查看整个项目代码的唯一方法是生成此项目，并在 \<project name>.asdatabase 文件中查看 ASSL 代码。  
  
### 查看对象的 XML 代码  
  
1.  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中打开 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]项目。  
  
2.  在解决方案资源管理器中右键单击对象，再单击“查看代码”。  
  
     将在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中显示此对象的 XML 代码。  
  
## 另请参阅  
 [生成 Analysis Services 项目 (SSDT)](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)  
  
  