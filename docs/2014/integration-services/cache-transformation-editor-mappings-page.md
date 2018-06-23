---
title: 缓存转换编辑器 （映射页） |Microsoft 文档
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
- sql12.dts.designer.cachetransmap.f1
ms.assetid: ffd53f18-9646-458a-a84a-f2467d601ea5
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 17e8b9894ddd1aa375a16703bced5d0cf05b77bb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017376"
---
# <a name="cache-transformation-editor-mappings-page"></a>缓存转换编辑器（“映射”页）
  可以使用 **“缓存转换编辑器”** 的 **“映射”** 页，将“缓存转换”转换中的输入列映射到缓存连接管理器中的目标列。  
  
> [!NOTE]  
>  每个输入列都必须映射到目标列，而且二者的列数据类型必须匹配。 否则， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 设计器将显示一则错误消息。  
  
 若要了解有关缓存转换的详细信息，请参阅 [Cache Transform](data-flow/transformations/cache-transform.md)。  
  
 若要了解有关缓存连接管理器的详细信息，请参阅 [Cache Connection Manager](connection-manager/cache-connection-manager.md)。  
  
## <a name="options"></a>“常规”  
 **可用输入列**  
 查看可用输入列的列表。 使用拖放操作将可用输入列映射到目标列。  
  
 还可以用键盘通过以下方法将输入列映射到目标列：突出显示 **“可用输入列”** 表中的某一列，按菜单键，然后选择 **“通过匹配名称映射项”**。  
  
 **可用目标列**  
 查看可用目标列的列表。 使用拖放操作将可用目标列映射到输入列。  
  
 还可以用键盘通过以下方法将输入列映射到目标列：突出显示 **“可用目标列”** 表中的某一列，按菜单键，然后选择 **“通过匹配名称映射项”**。  
  
 **输入列**  
 查看本主题中以前选择的输入列。 可以通过使用 **“可用输入列”** 列表来更改映射。  
  
 **目标列**  
 查看每个可用的目标列。  
  
## <a name="see-also"></a>请参阅  
 [缓存转换编辑器&#40;连接管理器页&#41;](../../2014/integration-services/cache-transformation-editor-connection-manager-page.md)  
  
  