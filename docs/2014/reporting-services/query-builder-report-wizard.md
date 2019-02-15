---
title: 查询生成器 （报表向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.dataview.vdtquerydesigner.f1
- sql12.rtp.rptwizard.querybuilder.f1
helpviewer_keywords:
- Query Builder [Reporting Services]
ms.assetid: 1b0904ea-28c1-448e-b56c-c0fdfbc8b222
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 358a82555a2f0b3df8a7635cb3ff39a7b09f2e50
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56290395"
---
# <a name="query-builder-report-wizard"></a>查询生成器（报表向导）
  使用查询生成器可以指定用于检索要在报表中使用的结果集的查询。 您可以在两种查询生成器中进行选择：  
  
-   基于文本的查询生成器（默认情况下）提供一个用于指定查询和查看结果的简单工作区。 您可以指定多个 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句，为自定义数据处理扩展插件指定查询或命令语法，还可以指定指定为表达式的查询。 由于一般查询生成器不对查询进行预处理，并且适用于任何类型的查询语法，所以用作报表设计器的默认查询生成器工具。  
  
-   图形查询生成器为用户提供了更为丰富的视觉体验。 该生成器用于 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的其他部分。 如果您创建的不是表达式或多部分的 SQL 语句，则可以使用图形查询生成器。  
  
     若要切换到图形查询生成器，请切换窗口左上角的 **“编辑为文本”** 按钮。  
  
 还可以从另一个报表导入查询。  
  
## <a name="query-builder-options"></a>查询生成器选项  
 **编辑为文本**  
 在基于文本的查询设计器和图形查询设计器之间切换（如果二者都适用于该查询）。  
  
 **导入**  
 打开“导入查询”对话框，显示任何可用报表的 .rdl 和 .sql 文件。 可以按原样使用导入的查询，也可以在查询生成器中进行修改。  
  
 **运算符(Run)**  
 运行查询，并且在查询有效的情况下返回结果集。 请注意，如果查询是表达式，您将不能执行查询。 若要验证基于表达式的查询，您必须预览报表。  
  
 **命令类型**  
 指定 Text、StoredProcedure 或 TableDirect。 命令类型是否可用取决于您指定的数据处理扩展插件。  
  
 **查询窗格**  
 键入查询。  
  
 **结果窗格**  
 显示查询返回的结果集。  
  
## <a name="see-also"></a>请参阅  
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [报表向导帮助](../../2014/reporting-services/report-wizard-help.md)  
  
  
