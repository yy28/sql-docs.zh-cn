---
title: 字词提取转换编辑器 （排除选项卡） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termextraction.inclusionexclusion.f1
helpviewer_keywords:
- Term Extraction Transformation Editor
ms.assetid: 90110d95-fd97-4542-9cda-832c86606130
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3a96d82cf2296fa8b0775e4fac025ebb53577344
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48201567"
---
# <a name="term-extraction-transformation-editor-exclusion-tab"></a>字词提取转换编辑器（“排除”选项卡）
  可以使用 **“字词提取转换编辑器”** 对话框的 **“排除”** 选项卡，建立与排除表的连接并指定包含排除字词的列。  
  
 若要了解有关字词提取转换的详细信息，请参阅 [Term Extraction Transformation](data-flow/transformations/term-extraction-transformation.md)。  
  
## <a name="options"></a>选项  
 **使用排除字词**  
 指示在字词提取过程中是否通过指定包含排除字词的列来排除特定的字词。 如果选择要排除字词，则必须指定以下源属性：  
  
 **“无缓存”**  
 选择现有的 OLE DB 连接管理器，或通过单击“新建”创建新的连接。  
  
 **新建**  
 通过使用“配置 OLE DB 连接管理器”对话框创建与数据库的新连接。  
  
 **表或视图**  
 选择包含排除字词的表或视图。  
  
 **列**  
 在表或视图中选择包含排除字词的列。  
  
 **配置错误输出**  
 使用[“配置错误输出” ](../../2014/integration-services/configure-error-output.md) 对话框可以为导致错误的行指定错误处理方式。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [字词提取转换编辑器&#40;字词提取选项卡&#41;](../../2014/integration-services/term-extraction-transformation-editor-term-extraction-tab.md)   
 [字词提取转换编辑器&#40;高级选项卡&#41;](../../2014/integration-services/term-extraction-transformation-editor-advanced-tab.md)   
 [字词查找转换](data-flow/transformations/lookup-transformation.md)  
  
  
