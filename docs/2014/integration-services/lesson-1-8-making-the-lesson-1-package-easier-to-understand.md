---
title: 步骤 8：使第 1 课包更易于理解 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e3751e53-77c7-47d0-8fe8-73ed1a53413a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 390fb10287ff88ec5f7a0220dea6dd677e8e36cd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62767589"
---
# <a name="step-8-making-the-lesson-1-package-easier-to-understand"></a>步骤 8：使 Lesson 1 包更易理解
  因为您已完成了 Lesson 1 包的配置，所以整理包布局是很必要的。 如果控制流和数据流布局中的形状大小不一，或者如果形状未对齐或未进行分组，则可能很难理解包功能。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Data Tools 提供的工具可让你轻松快速地设置包布局的格式。 格式设置功能包括使形状大小统一，对齐各个形状，并控制形状之间的水平间距和垂直间距。  
  
 另一种增进对包功能的了解的方式是添加描述包功能的批注。  
  
 在本任务中，您将使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools 中的格式设置功能改善数据流的布局并向数据流中添加批注。  
  
### <a name="to-format-the-layout-of-the-data-flow"></a>设置数据流布局的格式  
  
1.  如果尚未打开 Lesson 1 包，则请在解决方案资源管理器中双击 Lesson 1.dtsx。  
  
2.  单击 **“数据流”** 选项卡。  
  
3.  将游标置于 Extract Sample Currency 转换的右上方，单击并将游标拖过所有的数据流组件。  
  
4.  在 **“格式”** 菜单中，指向 **“使大小相同”**，再单击 **“两者”**。  
  
5.  选定数据流对象后，在 **“格式”** 菜单中，指向 **“对齐”**，再单击 **“左对齐”**。  
  
### <a name="to-add-an-annotation-to-the-data-flow"></a>向数据流中添加批注  
  
1.  右键单击数据流设计图面背景的任意位置，再单击 **“添加批注”**。  
  
2.  在批注框中键入或粘贴以下文本。  
  
     **The data flow extracts data from a file, looks up values in the CurrencyKey column in the DimCurrency table and the DateKey column in the DimDate table, and writes the data to the NewFactCurrencyRate table.**  
  
     若要在批注框中使文本换行，请将游标置于要开始新行的位置，然后按 Enter 键。  
  
     如果未将文本添加到批注框，则当您在批注框外部单击时，该文本便会消失。  
  
## <a name="next-steps"></a>后续步骤  
 [步骤 9：测试 Lesson 1 教程包](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
  
