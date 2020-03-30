---
title: “表达式”页 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.expressionspage.f1
helpviewer_keywords:
- Expressions Page dialog box
ms.assetid: c9016ec6-11c1-4ebd-b2a7-0fa6631fd9e4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9e3bbe6e788512144211ed35d1cfa8326d8f3ef7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "71290019"
---
# <a name="expressions-page"></a>“表达式”页

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  可以使用 **“表达式”** 页编辑属性表达式以及访问 **“属性表达式编辑器”** 和 **“属性表达式生成器”** 对话框。  
  
 属性表达式将在包运行时更新属性的值。 包、任务、容器、连接管理器以及一些数据流组件的属性可以使用属性表达式。 系统将对表达式求值，并且其结果将用来代替您在配置包和包对象时所设的属性的值。 表达式可以包含表达式语言所提供的变量、函数和运算符。 例如，可将一个包含“Weather forecast for”字符串的变量的值和 GETDATE() 函数的返回结果连接在一起形成字符串“Weather forecast for 4/5/2006”，从而为“发送邮件”任务生成主题行。  
  
 了解有关编写表达式和使用属性表达式的详细信息，请参阅 [Integration Services (SSIS) 表达式](../../integration-services/expressions/integration-services-ssis-expressions.md) 和 [在包中使用属性表达式](../../integration-services/expressions/use-property-expressions-in-packages.md)。  
  
## <a name="options"></a>选项  
 **表达式 (...)**  
 单击省略号可以打开 **“属性表达式编辑器”** 对话框。 有关详细信息，请参阅 [Property Expressions Editor](../../integration-services/expressions/property-expressions-editor.md)。  
  
 **\<属性名称>**  
 单击省略号可以打开 **“表达式生成器”** 对话框。 有关详细信息，请参阅 [Expression Builder](../../integration-services/expressions/expression-builder.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)   
 [系统变量](../../integration-services/system-variables.md)   
 [Integration Services (SSIS) 表达式](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
