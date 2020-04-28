---
title: 评估报表（SybaseToSQL） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: af24f2c4-5e86-4135-a4f3-a24faaeeefe7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c6d83e81253430f243fcaed55b66f6d0de6299ca
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68083506"
---
# <a name="assessment-report-sybasetosql"></a>评估报表 (SybaseToSQL)
"评估报告" 窗口显示了将数据库对象转换为[!INCLUDE[tsql](../../includes/tsql-md.md)]语法的结果，还可以帮助您估算迁移项目的复杂性和成本。  
  
若要访问评估报表，请在源元数据资源管理器中选择要转换的对象，右键单击 "**数据库**"，然后选择 "**创建报表**"。  
  
## <a name="options"></a>选项  
**转换统计信息**  
按语句类型显示转换统计信息。 此窗格仅在左窗格中选择了组对象（如架构）或没有代码的对象时可见。  
  
**按类别分类的对象**  
按对象类型显示转换统计信息。 此窗格仅在左窗格中选择了组对象（如架构）或没有代码的对象时可见。  
  
**统计信息**  
显示所选对象的转换统计信息。 仅当在左窗格中选择了具有代码的单个对象时，才会显示此窗格。 你可能需要展开 "**统计信息**" 以查看此窗格。  
  
**源导航**  
显示所选对象的 ASE 代码，并突出显示未转换为[!INCLUDE[tsql](../../includes/tsql-md.md)]的代码。 仅当在左窗格中选择了具有代码的单个对象时，才会显示此窗格。  
  
单击行号以设置或清除书签。 使用窗格顶部的按钮可以在代码中导航。  
  
**目标导航**  
显示所选对象的[!INCLUDE[tsql](../../includes/tsql-md.md)]转换结果代码，以及未转换的代码的错误消息。 仅当在左窗格中选择了具有代码的单个对象时，才会显示此窗格。  
  
单击行号以设置或清除书签。 使用窗格顶部的按钮可以在代码中导航。  
  
**消息窗格 (Messages pane)**  
显示在创建评估报告时生成的错误、警告和信息消息。 消息按数字进行分组。 若要查看导致错误的代码，请单击 "**错误**"、"**警告**" 或 "**信息**"，展开 "消息类别"，然后单击一条消息。  
  
