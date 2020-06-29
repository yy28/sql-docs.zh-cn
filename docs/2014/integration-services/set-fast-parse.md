---
title: 设置快速分析 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: dcd1dc09-6eaf-440b-9ce6-fef779ff794f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e6ff2c6ecd536dd5ecc34dceb358ffcf578ff3a7
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421724"
---
# <a name="set-fast-parse"></a>设置快速分析
  必须为使用快速分析的源或转换的每个列设置快速分析属性。 若要设置该属性，请使用平面文件源和数据转换的高级编辑器。  
  
### <a name="to-set-fast-parse"></a>设置快速分析  
  
1.  右键单击平面文件源或数据转换，然后单击“显示高级编辑器”。****  
  
2.  在 **“高级编辑器”** 对话框中，单击 **“输入属性和输出属性”** 选项卡。  
  
3.  在 **“输入和输出”** 窗格中，单击要为其启用快速分析的列。  
  
4.  在属性窗口中，展开 "**自定义属性**" 节点，然后将 `FastParse` 属性设置为 `True` 。  
  
5.  单击 **“确定”** 。  
  
  
