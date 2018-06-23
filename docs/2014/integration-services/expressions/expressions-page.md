---
title: “表达式”页 | Microsoft Docs
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
- sql12.dts.designer.expressionspage.f1
helpviewer_keywords:
- Expressions Page dialog box
ms.assetid: c9016ec6-11c1-4ebd-b2a7-0fa6631fd9e4
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: a266929860877c960c656033c41715154b6e2736
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123880"
---
# <a name="expressions-page"></a>“表达式”页
  可以使用 **“表达式”** 页编辑属性表达式以及访问 **“属性表达式编辑器”** 和 **“属性表达式生成器”** 对话框。  
  
 属性表达式将在包运行时更新属性的值。 包、任务、容器、连接管理器以及一些数据流组件的属性可以使用属性表达式。 系统将对表达式求值，并且其结果将用来代替您在配置包和包对象时所设的属性的值。 表达式可以包含表达式语言所提供的变量、函数和运算符。 例如，可将一个包含“Weather forecast for”字符串的变量的值和 GETDATE() 函数的返回结果连接在一起形成字符串“Weather forecast for 4/5/2006”，从而为“发送邮件”任务生成主题行。  
  
 若要了解有关编写表达式和使用属性表达式的详细信息，请参阅[Integration Services &#40;SSIS&#41;表达式](integration-services-ssis-expressions.md)和[使用 Property Expressions in Packages](use-property-expressions-in-packages.md)。  
  
## <a name="options"></a>“常规”  
 **表达式 (...)**  
 单击省略号可以打开 **“属性表达式编辑器”** 对话框。 有关详细信息，请参阅 [Property Expressions Editor](property-expressions-editor.md)。  
  
 **\<属性名称>**  
 单击省略号可以打开 **“表达式生成器”** 对话框。 有关详细信息，请参阅 [Expression Builder](expression-builder.md)。  
  
## <a name="see-also"></a>请参阅  
 [Integration Services &#40;SSIS&#41;变量](../integration-services-ssis-variables.md)   
 [系统变量](../system-variables.md)   
 [Integration Services (SSIS) 表达式](integration-services-ssis-expressions.md)  
  
  