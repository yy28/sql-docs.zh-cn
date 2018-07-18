---
title: 其他脚本组件示例 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], examples
ms.assetid: 849dd38a-abb5-4702-a413-882aae3980a5
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6d130773171edbf18fc8913e07317eeb92bfc66e
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2018
ms.locfileid: "35410169"
---
# <a name="additional-script-component-examples"></a>其他脚本组件示例
  脚本组件是一个可配置的工具，您可以在包的数据流中使用，它可以满足几乎所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 附带的源、转换和目标所无法满足的要求。 本节包含一些脚本组件代码示例，这些示例演示了各种类型的可用功能。  
  
 若要查看演示将脚本组件配置为基本的源、转换或目标的示例，请参阅[开发特定类型的脚本组件](../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)。  
  
> [!NOTE]  
>  如果希望创建可更方便地重用于多个数据流文件和多个包的组件，请考虑以这些脚本组件示例中的代码为基础，创建自定义数据流组件。 有关详细信息，请参阅 [开发自定义数据流组件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [模拟脚本组件的错误输出](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)  
 脚本组件不支持标准错误输出，但您可以通过少量的其他配置和编码来模拟标准错误输出。  
  
 [使用脚本组件增强错误输出](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md)  
 说明并演示如何使用脚本组件来向标准错误输出添加其他信息。  
  
 [使用脚本组件创建 ODBC 目标](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/creating-an-odbc-destination-with-the-script-component.md)  
 说明并演示如何使用脚本组件来创建 ODBC 数据流目标。  
  
 [使用脚本组件分析非标准文本文件格式](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/parsing-non-standard-text-file-formats-with-the-script-component.md)  
 说明并演示如何分析两种不同的非标准文本文件格式并将分析结果保存到目标表中。  
  
  
