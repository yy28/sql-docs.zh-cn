---
title: 查看 Analysis Services 项目 (SSDT) 的 XML |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- projects [Analysis Services], viewing XML
ms.assetid: dd1a4bc6-57b5-47df-8619-09f921aa6351
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ff8c70b2a4cd98fe665ca40bb95af8fa986bb6fc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48193417"
---
# <a name="view-the-xml-for-an-analysis-services-project-ssdt"></a>查看 Analysis Services 项目的 XML (SSDT)
  在项目模式下使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库时， [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 为项目文件夹中的每个对象创建 XML 定义。 您可以查看 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中每个对象的 XML 文件的内容， 还可以直接编辑 XML 文件；但是，大多数情况下不建议这样做，因为您所做的更改可能会使 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]无法读取 XML。  
  
> [!NOTE]  
>  您无法查看整个项目的 XML 代码，但是可以查看每个对象的代码，因为每个对象都有单独的文件。 中的代码的唯一的方法，若要查看整个项目是生成项目并查看 ASSL 代码\<项目名称 >.asdatabase 文件。  
  
### <a name="to-view-the-xml-code-for-an-object"></a>查看对象的 XML 代码  
  
1.  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中打开 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]项目。  
  
2.  在解决方案资源管理器中右键单击对象，再单击“查看代码”。  
  
     将在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中显示此对象的 XML 代码。  
  
## <a name="see-also"></a>请参阅  
 [生成 Analysis Services 项目&#40;SSDT&#41;](build-analysis-services-projects-ssdt.md)  
  
  
