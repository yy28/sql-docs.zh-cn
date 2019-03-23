---
title: 其他脚本组件示例 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], examples
ms.assetid: 849dd38a-abb5-4702-a413-882aae3980a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f0cab4451b78b662a426612aee0f0a72aae8cf80
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58393875"
---
# <a name="additional-script-component-examples"></a>其他脚本组件示例
  脚本组件是一个可配置的工具，您可以在包的数据流中使用，它可以满足几乎所有 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 附带的源、转换和目标所无法满足的要求。 本节包含一些脚本组件代码示例，这些示例演示了各种类型的可用功能。  
  
 若要查看演示将脚本组件配置为基本的源、转换或目标的示例，请参阅[开发特定类型的脚本组件](../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)。  
  
> [!NOTE]  
>  如果希望创建可更方便地重用于多个数据流文件和多个包的组件，请考虑以这些脚本组件示例中的代码为基础，创建自定义数据流组件。 有关详细信息，请参阅 [开发自定义数据流组件](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)。  
  
## <a name="in-this-section"></a>本节内容  
 [模拟脚本组件的错误输出](../extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)  
 脚本组件不支持标准错误输出，但您可以通过少量的其他配置和编码来模拟标准错误输出。  
  
 [使用脚本组件增强错误输出](../extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md)  
 说明并演示如何使用脚本组件来向标准错误输出添加其他信息。  
  
 [使用脚本组件创建 ODBC 目标](../extending-packages-scripting-data-flow-script-component-examples/creating-an-odbc-destination-with-the-script-component.md)  
 说明并演示如何使用脚本组件来创建 ODBC 数据流目标。  
  
 [使用脚本组件分析非标准文本文件格式](../extending-packages-scripting-data-flow-script-component-examples/parsing-non-standard-text-file-formats-with-the-script-component.md)  
 说明并演示如何分析两种不同的非标准文本文件格式并将分析结果保存到目标表中。  
  
![集成服务图标 （小）](../media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
  
