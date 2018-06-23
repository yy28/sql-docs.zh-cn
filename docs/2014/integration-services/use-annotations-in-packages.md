---
title: 在包中使用批注 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- self-documenting packages
- adding annotations
- annotations [Integration Services]
ms.assetid: 48c8ed9a-b10d-490c-9ba7-4b77aa44e3dd
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f00ac9f1013bbf9b95999f51631970f9935364c7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026149"
---
# <a name="use-annotations-in-packages"></a>在包中使用批注
  [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器提供批注，利用它们可使包自文档化，且更易理解和维护。 可以将批注添加到 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器的控制流、数据流和事件处理程序设计图面。 批注可以包含任何类型的文本，对将标签、注释和其他说明性信息添加到包十分有用。 批注仅为设计时功能。 例如，批注不会写入日志。  
  
 按 Enter 时，文本会换行到下一行。 在添加其他文本行时，批注框的大小会自动增加。 包批注会以明文形式持久保持在包文件的 CDATA 部分。  
  
 有关更改包文件格式的详细信息，请参阅 [SSIS 包格式](../../2014/integration-services/ssis-package-format.md)。  
  
 保存包时， [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器将批注保存在包中。  
  
### <a name="to-add-an-annotation-to-a-package"></a>将批注添加到包  
  
-   [将批注添加到包](../../2014/integration-services/add-an-annotation-to-a-package.md)  
  
  