---
title: 在包中使用批注 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- self-documenting packages
- adding annotations
- annotations [Integration Services]
ms.assetid: 48c8ed9a-b10d-490c-9ba7-4b77aa44e3dd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 767340b1c888c9cc25bad494ae13ae8559be31ac
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295051"
---
# <a name="use-annotations-in-packages"></a>在包中使用批注

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器提供批注，利用它们可使包自文档化，且更易理解和维护。 可以将批注添加到 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器的控制流、数据流和事件处理程序设计图面。 批注可以包含任何类型的文本，对将标签、注释和其他说明性信息添加到包十分有用。 批注仅为设计时功能。 例如，批注不会写入日志。  
  
 按 Enter 时，文本会换行到下一行。 在添加其他文本行时，批注框的大小会自动增加。 包批注会以明文形式持久保持在包文件的 CDATA 部分。  
  
 有关更改包文件格式的详细信息，请参阅 [SSIS 包格式](https://msdn.microsoft.com/library/cfe0e5dc-5be3-4222-b721-fe83665edd94)。  
  
 保存包时， [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器将批注保存在包中。  
  
## <a name="add-an-annotation-to-a-package"></a>将批注添加到包  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，打开包含要添加批注的包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目。  
  
2.  在解决方案资源管理器中，双击该包将其打开。  
  
3.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中，右键单击“控制流”  、“数据流”  或“事件处理程序”  选项卡上设计图面的任意处，再单击“添加批注”  。 选项卡的设计图面上将出现文本块。  
  
4.  添加文本。  
  
    > [!NOTE]  
    >  如果未添加文本，则单击文本块外部时此文本块会被删除。  
  
5.  若要更改批注中的文本大小或格式，请右键单击该批注，然后单击“设置文本批注字体”  。  
  
6.  若要添加其他文本行，请按 Enter。  
  
     在添加其他文本行时，批注框的大小会自动增加。  
  
7.  若要向组添加批注，请右键单击该批注，然后单击“组”  。  
  
8.  若要保存更新后的包，请单击 **“文件”** 菜单中的 **“全部保存”** 。  
