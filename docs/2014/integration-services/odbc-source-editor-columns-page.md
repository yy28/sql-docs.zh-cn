---
title: ODBC 源编辑器 （列页） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.columns.f1
ms.assetid: 565984eb-8318-4be7-bebc-262209cf5065
caps.latest.revision: 6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b16be16730643cc063b39594c8e01f1321b6a983
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37209427"
---
# <a name="odbc-source-editor-columns-page"></a>ODBC 源编辑器（“列”页）
  可以使用“ODBC 源编辑器”对话框的“列”页，将输出列映射到每个外部（源）列。  
  
 若要了解有关 ODBC 源的详细信息，请参阅 [ODBC Source](data-flow/odbc-source.md)。  
  
## <a name="task-list"></a>任务列表  
 **打开“ODBC 源编辑器”的“列”页**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]中，打开具有 ODBC 源的 [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] 包。  
  
2.  在“数据流”选项卡上，双击 ODBC 源。  
  
3.  在 **“ODBC 源编辑器”** 中，单击 **“列”**。  
  
## <a name="options"></a>“常规”  
  
### <a name="available-external-columns"></a>可用外部列  
 数据源中的可用外部列的列表。 无法使用此表添加或删除列。 从源中选择要使用的列。 所选列将按照选择它们时的顺序添加到 **“外部列”** 列表中。  
  
 选中 **“全选”** 复选框可以选择所有列。  
  
### <a name="external-column"></a>外部列  
 外部（源）列的视图，该视图按照您在配置使用 ODBC 源中数据的组件时所看到的列顺序显示。  
  
### <a name="output-column"></a>输出列  
 输入每个输出列的唯一名称。 默认值为所选外部（源）列的名称；不过，您也可以任选一个唯一的描述性名称。 输入的名称显示在 SSIS 设计器中。  
  
## <a name="see-also"></a>请参阅  
 [ODBC 源编辑器&#40;连接管理器页&#41;](../../2014/integration-services/odbc-source-editor-connection-manager-page.md)   
 [ODBC 源编辑器&#40;错误输出页&#41;](../../2014/integration-services/odbc-source-editor-error-output-page.md)  
  
  
