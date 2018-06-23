---
title: 程序集属性对话框 (Analysis Services-多维数据) |Microsoft 文档
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
- sql12.asvs.sqlserverstudio.assemblyproperties.f1
ms.assetid: da1174d6-d82b-4337-ac19-7368dbd95a84
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fa00c8753e30926113d90881401a8b38e573e6b8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028693"
---
# <a name="assembly-properties-dialog-box-analysis-services---multidimensional-data"></a>“程序集属性”对话框（Analysis Services - 多维数据）
  可以使用 **中的** “程序集属性” [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 对话框，设置 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库中的程序集引用的属性。 通过在“对象资源管理器”中右键单击某个程序集，并选择“属性”，可以显示“程序集属性”对话框。  
  
## <a name="options"></a>“常规”  
  
|术语|定义|  
|----------|----------------|  
|**名称**|键入内容即可更改程序集引用的名称。<br /><br /> 注意：更改此值不会更改程序集引用所表示引用的程序集的名称，但会更改 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例或数据库在表示程序集引用时所使用的名称。|  
|**ID**|显示程序集引用所引用的程序集的标识符。|  
|**Description**|键入内容即可更改程序集引用的名称。|  
|**创建时间戳**|显示程序集引用的创建日期和时间。|  
|**上次架构更新时间**|显示上次更新程序集引用的元数据的日期和时间。|  
|**类型**|显示程序集引用的类型。 将显示以下值：<br /><br /> **.NET 程序集**： 程序集引用是指[!INCLUDE[msCoName](../includes/msconame-md.md)].NET Framework 程序集。<br /><br /> **COM DLL**： 程序集引用指 COM 库。|  
|**数据源**|显示程序集引用的源。 此属性通常包含程序集引用所引用的程序集的完整路径和文件名。|  
|**权限集**|选择用来确定对程序集引用的访问权限的权限集。 有关此属性的可用值的详细信息，请参阅<xref:Microsoft.AnalysisServices.ClrAssembly.PermissionSet%2A>。|  
|**模拟信息**|选择在访问程序集引用时要使用的模拟信息。 有关此属性的可用值的详细信息，请参阅 [ImpersonationInfo 元素 (ASSL)](scripting/properties/impersonationinfo-element-assl.md)|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [多维模型程序集管理](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  