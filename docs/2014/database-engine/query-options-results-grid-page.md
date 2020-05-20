---
title: 查询选项结果（网格页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.grid.f1
ms.assetid: 764bf435-3aab-4c62-b4e0-64fe020a5a95
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1d5696dcc7b82844fad52754f3c4457344eca793
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000577"
---
# <a name="query-options-results-grid-page"></a>“查询选项”中的“结果”（“网格”页）
  使用此页可以指定以网格格式显示查询结果集的选项。  
  
## <a name="options"></a>选项  
 **在结果集中包括查询**  
 将查询文本作为结果集的一部分返回。  
  
 **复制或保存结果时包括列标题**  
 将结果复制到剪贴板或保存到文件时，包括列标题。 如果希望保存或复制的结果数据只有数据而没有列标题，请清除此复选框。  
  
 **执行后放弃结果**  
 当屏幕显示接收到查询结果之后，通过放弃查询结果来释放内存。  
  
 **在单独选项卡中显示结果**  
 在新文档窗口中显示结果集，而不是在查询文档窗口的底部显示。  
  
 **执行查询后切换到“结果”选项卡**  
 自动将屏幕焦点设置到结果集。  
  
 **检索的最多字符数**  
 **非 XML 数据**：  
  
 输入一个介于 1 到 65535 之间的数字以指定每个单元中显示的最大字符数。  
  
> [!NOTE]  
>  指定大量字符可能会导致结果集中显示的数据截断。 每个单元中显示的最大字符数取决于字号。 在返回较大的结果集时，如果此框中的值太大，可能会导致 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 运行时内存不足，从而影响系统性能。  
  
 **XML 数据**：  
  
 选择**1 MB**、 **2 MB**或**5 mb**。 选择 "**无限制**" 将检索所有字符。  
  
 **重置为默认值**  
 将此页上的所有值重置为原始默认值。  
  
  
