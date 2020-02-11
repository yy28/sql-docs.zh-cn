---
title: 评估报表（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Assessment Report dialog box
- Conversion Report dialog box
ms.assetid: ba6f53aa-0049-4c49-8bb8-607a8bfaa737
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c28fb4cf5d110e01b156fc6ce985b2cb2fb7bfe1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67910684"
---
# <a name="assessment-report-accesstosql"></a>评估报表（AccessToSQL）
"评估报告" 窗口显示了将数据库对象转换为[!INCLUDE[tsql](../../includes/tsql-md.md)]语法的结果，还可以帮助您估算迁移项目的复杂性和成本。  
  
若要创建评估报表，请在源元数据资源管理器中选择要转换的对象，右键单击 "**数据库**"，然后选择 "**创建报表**"。 在转换架构后，还可以自动显示此报告。 但是，报表名称将为转换报表。 有关详细信息，请参阅[项目设置（GUI）（SSMA 通用）](https://msdn.microsoft.com/cf06baf1-8714-48a3-95dc-781f6ca53693)。  
  
## <a name="options"></a>选项  
**“资源管理器”窗格**  
包含评估报表中对象的层次结构。 展开文件夹以查看各个对象和子组件。 单击类别或对象时，该类别或对象的转换统计信息将显示在 "详细信息" 窗格中。  
  
**详细信息窗格**  
显示所选对象的转换统计信息或错误和警告消息。 例如，如果选择了 "表" 文件夹，则详细信息窗格将显示已转换的外键、索引、主键和表的数目。  
  
**消息窗格 (Messages pane)**  
显示在创建评估报告时生成的错误、警告和信息消息。 消息按数字进行分组。  
  
若要查看消息详细信息，请单击 "**错误**"、"**警告**" 或 "**消息**"，然后展开消息。 SSMA 将显示具有此错误的对象的列表。 单击对象以显示对象的所有转换详细信息。  
  
## <a name="see-also"></a>另请参阅  
[用户界面参考（访问）](https://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  
