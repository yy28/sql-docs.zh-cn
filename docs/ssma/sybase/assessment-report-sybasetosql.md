---
title: 评估报表 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: af24f2c4-5e86-4135-a4f3-a24faaeeefe7
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 11b47065fe180956d58361ec80eda1dac25fa4b1
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "87932318"
---
# <a name="assessment-report-sybasetosql"></a>评估报表 (SybaseToSQL)
"评估报告" 窗口显示了将数据库对象转换为语法的结果 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，还可以帮助您估算迁移项目的复杂性和成本。  
  
若要访问评估报表，请在源元数据资源管理器中选择要转换的对象，右键单击 "**数据库**"，然后选择 "**创建报表**"。  
  
## <a name="options"></a>选项  
**转换统计信息**  
按语句类型显示转换统计信息。 此窗格仅在左窗格中选择了组对象（如架构）或没有代码的对象时可见。  
  
**按类别分类的对象**  
按对象类型显示转换统计信息。 此窗格仅在左窗格中选择了组对象（如架构）或没有代码的对象时可见。  
  
**统计信息**  
显示所选对象的转换统计信息。 仅当在左窗格中选择了具有代码的单个对象时，才会显示此窗格。 你可能需要展开 "**统计信息**" 以查看此窗格。  
  
**源导航**  
显示所选对象的 ASE 代码，并突出显示未转换为的代码 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 仅当在左窗格中选择了具有代码的单个对象时，才会显示此窗格。  
  
单击行号以设置或清除书签。 使用窗格顶部的按钮可以在代码中导航。  
  
**目标导航**  
显示 [!INCLUDE[tsql](../../includes/tsql-md.md)] 所选对象的转换结果代码，以及未转换的代码的错误消息。 仅当在左窗格中选择了具有代码的单个对象时，才会显示此窗格。  
  
单击行号以设置或清除书签。 使用窗格顶部的按钮可以在代码中导航。  
  
**消息窗格 (Messages pane)**  
显示在创建评估报告时生成的错误、警告和信息消息。 消息按数字进行分组。 若要查看导致错误的代码，请单击 "**错误**"、"**警告**" 或 "**信息**"，展开 "消息类别"，然后单击一条消息。  
  
