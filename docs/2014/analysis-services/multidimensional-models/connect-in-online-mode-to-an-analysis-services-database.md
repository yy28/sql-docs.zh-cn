---
title: 以联机模式连接到 Analysis Services 数据库 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, connecting
ms.assetid: 33041234-7106-404f-a289-8e904f32aff2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 37b28b6d4f15e29242d20b33bb5ade12460ded7e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076572"
---
# <a name="connect-in-online-mode-to-an-analysis-services-database"></a>在联机模式下连接到 Analysis Services 数据库
  可以直接连接到现有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库并直接修改该数据库中的对象。 直接连接到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库时，会立即更改对象并且不在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中创建 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]项目。  
  
### <a name="to-connect-directly-to-an-analysis-services-database-by-using-sql-server-data-tools"></a>使用 SQL Server Data Tools 直接连接到 Analysis Services 数据库  
  
1.  打开 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]。  
  
2.  在 **“文件”** 菜单上，指向 **“打开”** ，然后单击 **“Analysis Services 数据库”** 。  
  
3.  选择 **“连接到现有数据库”** 。  
  
4.  指定服务器名称和数据库名称。  
  
     可以键入数据库名称，也可以查询服务器以查看服务器上的现有数据库。  
  
5.  单击“确定”  。  
  
     现在可以直接编辑 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中的所有对象。  
  
## <a name="see-also"></a>请参阅  
 [在开发阶段使用 Analysis Services 项目和数据库](work-with-analysis-services-projects-and-databases-in-development.md)   
 [使用 SQL Server Data Tools 创建多维模型 (SSDT)](creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)  
  
  
