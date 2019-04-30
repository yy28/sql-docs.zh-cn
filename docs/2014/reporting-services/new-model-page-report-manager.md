---
title: 新模型页 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 27d5bf66-b0e7-489e-a830-ffe2ec8e5350
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b0d571210c44026fc34ab43cb07e18bbd8526ed5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188415"
---
# <a name="new-model-page-report-manager"></a>“新建模型”页（报表管理器）
  使用此页可以从共享数据源生成默认的报表模型。 只能从 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 多维数据源、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 关系数据源和 Oracle 关系数据源生成报表模型。  
  
 在报表管理器中生成的模型基于共享数据源的架构。 将为数据源中的所有表和列创建实体、文件夹和字段。 您既不能排除项，也不能设置用于决定如何生成模型的选项。 如果要自定义或完善模型，则必须改用模型设计器。  
  
## <a name="navigation"></a>导航  
 使用以下过程导航到用户界面 (UI) 中的这一位置。  
  
###### <a name="to-open-the-new-model-page"></a>打开“新建模型”页  
  
1.  打开报表管理器，找到您要从中生成模型的共享数据源。  
  
2.  悬停在该数据源之上，然后单击下拉箭头。  
  
3.  在下拉菜单中，执行以下步骤之一：  
  
    -   单击 **“生成报表模型”** 以打开“新建模型”页。  
  
    -   单击 **“管理”** 以打开报表的“常规属性”页。 然后，单击 **“生成模型”** 以打开“新建模型”页。  
  
## <a name="options"></a>选项  
 **名称**  
 指定模型的名称。 名称必须至少包含一个字母数字字符。 还可以包含空格和某些符号。 在指定名称时请不要使用以下字符：  
  
 ; ? : \@ & = + , $ / * \< > | " /  
  
 **说明**  
 显示模型的说明。 通过报表管理器查看此项的用户在浏览文件夹层次结构时会看到此说明。  
  
 **更改位置**  
 显示新模型的文件夹位置。 可以单击 **“更改位置”** 按钮来选择其他位置。  
  
  
