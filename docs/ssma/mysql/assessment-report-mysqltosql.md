---
title: 评估报表（MySQLToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5525d989-024c-402d-9e84-faa4721cc5b9
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: fb6d01bf9c02d0a7b96adf8e46eb354cd426db4d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139193"
---
# <a name="assessment-report-mysqltosql"></a>评估报表 (MySQLToSQL)
"评估报告" 窗口显示了将数据库对象转换为[!INCLUDE[tsql](../../includes/tsql-md.md)]语法的结果，还可以帮助您估算迁移项目的复杂性和成本。  
  
若要访问评估报表，请在源元数据资源管理器中选择要转换的对象，右键单击 "**架构**"，然后选择 "**创建报表**"。  
  
## <a name="options"></a>选项  
  
|||  
|-|-|  
|**术语**|**定义**|  
|**转换统计信息**|按语句类型显示转换统计信息。 如果在左窗格中选择了组对象（如架构）或没有代码的对象，则将显示此窗格。|  
|**按类别分类的对象**|按类别显示对象的数量。 此窗格仅在左窗格中选择了组对象（如架构）或没有代码的对象时可见。|  
|**统计信息**|显示所选对象的转换统计信息。 仅当在左窗格中选择了具有代码的单个对象时，才会显示此窗格。 你可能需要展开 "**统计信息**" （位于**源**窗格的紧上方）才能查看此窗格。|  
|**数据源**|显示所选对象的 MySQL 代码，并突出显示未转换为[!INCLUDE[tsql](../../includes/tsql-md.md)]的代码。 仅当在左窗格中选择了具有代码的单个对象时，才会显示此窗格。<br /><br />单击行号以设置或清除书签。 使用窗格顶部的按钮可以在代码中导航。|  
|**靶**|显示所选对象的[!INCLUDE[tsql](../../includes/tsql-md.md)]转换结果代码，以及未转换的代码的错误消息。 仅当在左窗格中选择了具有代码的单个对象时，才会显示此窗格。<br /><br />单击行号以设置或清除书签。 使用窗格顶部的按钮可以在代码中导航。|  
|**消息窗格 (Messages pane)**|显示在创建评估报告时生成的错误、警告和信息性消息。 消息按数字进行分组。 若要查看导致错误的代码，请单击 "**错误**"、"**警告**" 或 "**信息**"，展开 "消息类别"，然后单击一条消息。|  
  
