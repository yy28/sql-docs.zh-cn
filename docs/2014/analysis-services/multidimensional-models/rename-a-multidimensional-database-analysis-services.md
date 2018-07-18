---
title: 重命名多维数据库 (Analysis Services) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- renaming databases
ms.assetid: 15fdaec7-f3e4-44d9-9b78-1a1d78c484e0
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 192582ec7724e16b0c02d499fac89798c4c17cd6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37312657"
---
# <a name="rename-a-multidimensional-database-analysis-services"></a>重命名多维数据库 (Analysis Services)
  更改 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库名称的方式取决于如何连接 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。 若要更改现有数据库的名称，则必须在联机模式下进行连接。 若要更改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中要进行实例化的对象所在数据库的名称，必须以项目模式进行连接。  
  
### <a name="to-change-the-database-name-in-online-mode"></a>在联机模式下更改数据库名称  
  
1.  使用 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]，直接连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。  
  
2.  在解决方案资源管理器中，右键单击该数据库，再单击“编辑数据库”。  
  
3.  在 **“数据库名称”** 文本框中，更改数据库名称。  
  
4.  在工具栏上单击 **“保存”** 或 **“全部保存”** ，在 **“文件”** 菜单上单击 **“保存选定项”** 或 **“全部保存”** ，或者关闭 **数据库设计器** 并在出现提示时单击 **“保存”** 。  
  
     这样便会在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中更新数据库名称，并且会刷新解决方案资源管理器中的数据库对象。  
  
### <a name="to-change-the-database-name-in-project-mode"></a>在项目模式下更改数据库名称  
  
1.  打开 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，右键单击 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目，再单击“属性”。  
  
3.  在 **“属性页”** 对话框中，单击 **“配置属性”** 部分中的 **“部署”** 。  
  
4.  将 **“数据库”** 属性更改为新的数据库名称。  
  
     下次部署 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目时，会将其部署为这一新的数据库名称。 如果此数据库已存在，则会将其覆盖。  
  
### <a name="to-change-the-database-name-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 更改数据库名称  
  
-   右键单击 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库并且编辑 Name 属性。  
  
## <a name="see-also"></a>请参阅  
 [在 Analysis Services 中配置服务器属性](../server-properties/server-properties-in-analysis-services.md)   
 [设置多维数据库属性&#40;Analysis Services&#41;](set-multidimensional-database-properties-analysis-services.md)   
 [配置 Analysis Services 项目属性&#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md)   
 [部署 Analysis Services 项目&#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
  
