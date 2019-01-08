---
title: 报表属性对话框引用 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10530"
- sql12.rtp.rptdesigner.reportproperties.references.f1
ms.assetid: 4639d368-9918-4bb1-9953-7a724ca78dea
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 628a94ec8e8c79ec88f8427fd2ea41f158ae6c38
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52539796"
---
# <a name="report-properties-dialog-box-references"></a>“报表属性”对话框 ->“引用”
  选择 **“报表属性”** 对话框中的 **“引用”** 可以添加或删除对报表定义中的表达式所使用的自定义程序集或其他外部程序集以及自定义类实例的引用。  
  
## <a name="options"></a>选项  
 **添加或删除程序集**  
 列出报表引用的程序集。 该程序集在安装报表设计工具的计算机上以及报表服务器上必须可用。 引用的名称必须匹配的内容 **\<CodeModule >** 完全标记报表定义语言 (.rdl) 文件中。  
  
 **“添加”**  
 单击该选项可以添加程序集。 单击省略号 （...） 按钮以打开**打开**对话框并选择完成报表处理和表达式计算所需的程序集。  
  
 **删除**  
 若要从列表中删除程序集引用，请选择程序集名并单击“删除”按钮。  
  
 **添加或删除类**  
 列出报表使用的类实例。 该类列表仅适用于基于实例的成员，而不适用于静态成员。  
  
 **“添加”**  
 单击该选项可以添加类引用。 单击省略号 （...） 按钮以打开**打开**对话框并选择完成报表处理和表达式计算所需的类。  
  
 **删除**  
 若要删除类实例，请选中该实例并单击“删除”按钮。  
  
 **向上**  
 可为有依赖关系的类在列表中上移该引用。  
  
 **向下**  
 可为有依赖关系的类在列表中下移该引用。  
  
## <a name="see-also"></a>请参阅  
 [报表设计器的表达式中的自定义代码和程序集引用 (SSRS)](report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)   
 [报表和组变量集合引用（报表生成器和 SSRS）](report-design/built-in-collections-report-and-group-variables-references-report-builder.md)   
 [表达式示例（报表生成器和 SSRS）](report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
