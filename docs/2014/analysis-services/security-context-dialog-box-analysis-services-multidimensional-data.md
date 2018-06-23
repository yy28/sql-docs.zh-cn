---
title: 安全上下文对话框 (Analysis Services-多维数据) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.securitycontext.f1
ms.assetid: 238a4a4b-84bd-4b3d-9f02-f3adf57fa3af
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: dea478729f3ca99b63df6d94c90e062bb140dbf3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126921"
---
# <a name="security-context-dialog-box-analysis-services---multidimensional-data"></a>“安全上下文”对话框（Analysis Services - 多维数据）
  可以使用 **中的** “安全上下文” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 对话框，更改用于检查 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象的数据或元数据的用户和角色。 在多维数据集设计器的 **“计算”** 选项卡或 **“浏览器”** 选项卡上，单击 **“工具栏”** 窗格中的 **“安全上下文”** 可以显示 **“安全上下文”** 对话框。  
  
## <a name="options"></a>“常规”  
 **当前用户**  
 选择此选项可以在查看 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象的数据和元数据时使用当前用户的域和用户名。  
  
 **其他用户**  
 键入要在查看 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象的数据和元数据时使用的其他用户或组的域和用户名。  
  
 用户或组的域和用户名使用下面的格式：  
  
 *\<域名 >* **\\** *\<用户帐户名 >*  
  
 **Roles**  
 选择此选项可以在查看 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象的数据和元数据时使用一个或多个指定的角色。 如果在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库中定义了多个角色，则可以选择要使用的角色。  
  
## <a name="see-also"></a>请参阅  
 [Kpi&#40;多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)   
 [浏览器&#40;多维数据集设计器&#41; &#40;Analysis Services-多维数据&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)   
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  