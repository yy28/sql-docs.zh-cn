---
title: 使用 Analysis Services 项目和在生产环境中的数据库 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f90af41c397da20fb26c73bebc6723b9a3cf6270
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62743233"
---
# <a name="work-with-analysis-services-projects-and-databases-in-production"></a>使用 Analysis Services 项目和在生产环境中的数据库
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中开发 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库并将其部署到 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例之后，必须确定要如何对已部署数据库中的对象进行更改。 可以使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]进行与安全角色、分区和存储设置相关的特定更改。 其他更改则只能使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]在项目模式或联机模式下进行（例如添加属性或用户定义层次结构）。  
  
 一旦使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在联机模式下对已部署的 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 数据库进行更改，部署所用的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目便会立即成为过时项目。 如果开发人员在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目中进行了更改并尝试部署已修改的项目，则系统将会提示开发人员覆盖整个数据库。 如果开发人员覆盖整个数据库，则还必须对数据库进行处理。 如果生产人员在未与开发小组沟通的情况下直接对已部署的数据库进行更改，则此问题会变得更为复杂，因为生产人员将不理解为何他们的更改不再显示在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库中。  
  
 有多种方法使用 SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 工具来避免这种情况下存在的问题。  
  
-   方法 1:每当对生产版本进行更改[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库，请使用[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]若要创建一个新[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]基于修改后的版本的项目[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库。 可以将这一新的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 项目作为项目的主控副本签入到源代码管理系统。 无论是使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 还是 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 在联机模式下对 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 数据库进行更改，这种方法均行之有效。  
  
-   方法 2：对生产版本的唯一进行更改[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]在项目模式下。 借助这种方法，您可以使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署向导中可用的选项来保留由 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]所做的更改，例如安全角色和存储设置。 这样可确保将与设计相关的设置保留在项目文件中（可以忽略存储设置和安全角色），并将联机服务器用于存储设置和安全角色。  
  
-   方法 3:对生产版本的唯一进行更改[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数据库使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]在联机模式下。 由于这两种工具都仅使用相同的联机服务器，因此，不同版本也会保持同步。  
  
  
