---
title: 数据挖掘查询 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.dataminingquery.f1
ms.assetid: 948e358a-6245-429f-82c7-4cedc5e048fd
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 754c937ed8fa167a62f665368c47d9e9ee6a6bb7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025747"
---
# <a name="data-mining-query"></a>数据挖掘查询
  设计窗格包含数据挖掘预测查询生成器，可用于生成数据挖掘预测查询。 您可以基于输入表设计预测查询，也可以设计单独预测查询。 切换到结果视图可运行查询并查看结果。 查询视图将显示由预测查询生成器创建的数据挖掘扩展插件 (DMX) 查询。  
  
## <a name="options"></a>“常规”  
 “切换视图”按钮  
 单击图标可以在设计窗格和查询窗格之间切换。 默认情况下，设计窗格处于打开状态。  
  
 若要切换到设计窗格，请单击![设计图标](../media/ssis-designicon.gif "Design icon")图标。  
  
 若要切换到查询窗格，请单击 ![SQL 图标](../media/ssis-queryicon.gif "SQL icon")图标。  
  
 **挖掘模型**  
 显示所选的挖掘模型，您希望利用该模型来进行预测。  
  
 **选择模型**  
 打开“选择挖掘模型”对话框。  
  
 **输入列**  
 显示用于生成预测的所选输入列。  
  
 **数据源**  
 从下拉列表中选择包含要用于列的字段的源。 可以使用“挖掘模型”表中所选的挖掘模型、“选择输入表”表中所选的输入表、预测函数或自定义表达式。  
  
 可以将列从包含挖掘模型的表和输入列中拖动到单元。  
  
 **字段**  
 从派生自源表的列的列表中选择列。 如果在“源”中选择了“预测函数”，则此单元将包含对所选挖掘模型可用的预测函数的下拉列表。  
  
 **别名**  
 服务器返回的列的名称。  
  
 **显示**  
 选择此项将返回列或只使用 WHERE 子句中的列。  
  
 **分组**  
 与“和/或”列一起使用，将表达式组合到一起。 例如，(expr1 OR expr2) AND expr3。  
  
 **和/或**  
 用于创建逻辑查询。 例如，(expr1 OR expr2) AND expr3。  
  
 **条件/参数**  
 指定应用于该列的条件表达式或用户表达式。 可以将列从包含挖掘模型的表和输入列中拖动到单元。  
  
## <a name="see-also"></a>请参阅  
 [数据挖掘查询接口](../../analysis-services/data-mining/data-mining-query-tools.md)   
 [数据挖掘扩展插件 (DMX) 语句引用](/sql/dmx/data-mining-extensions-dmx-statements)  
  
  
