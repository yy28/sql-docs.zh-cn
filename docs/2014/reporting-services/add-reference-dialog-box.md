---
title: 添加引用对话框 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rtp.rptdesigner.addreference.f1
helpviewer_keywords:
- Edit References dialog box
ms.assetid: 7bdd2eee-195a-4a2f-a0aa-56f7e90c1fb4
caps.latest.revision: 27
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: ecf67f3b8c82ba63ee24aca05238e311f3ed36bf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129835"
---
# <a name="add-reference-dialog-box"></a>“添加引用”对话框
  使用 **“添加引用”** 对话框可以向报表添加对自定义程序集或 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 组件的引用。 添加程序集引用后，可以编写表达式或嵌入式自定义代码，其中包含对程序集或组件中的类或方法的完全限制引用。 有关详细信息，请参阅[报表设计器的表达式中的自定义代码和程序集引用 (SSRS)](report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md) 或[向报表添加程序集引用 (SSRS)](report-design/add-an-assembly-reference-to-a-report-ssrs.md)。  
  
## <a name="options"></a>“常规”  
 **.NET**  
 用于选择全局程序集缓存 (GAC) 中安装的 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 组件或程序集。  
  
 **“浏览”**  
 用于浏览文件系统上的外部程序集。  
  
> [!NOTE]  
>  如果要发布包含对外部程序集引用的报表，则必须先在报表服务器上安装该程序集，然后才能成功处理该报表。  
  
 **最新**  
 用于选择最近使用的程序集的名称。  
  
## <a name="see-also"></a>请参阅  
 [与报表中使用自定义程序集](custom-assemblies/using-custom-assemblies-with-reports.md)   
 [向报表添加代码 (SSRS)](report-design/add-code-to-a-report-ssrs.md)  
  
  