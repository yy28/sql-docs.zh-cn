---
title: "初始化自定义程序集对象 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- initializing custom assemblies [Reporting Services]
- custom assemblies [Reporting Services], initializing
- OnInit method
ms.assetid: 26fd74dc-d02f-40f7-aeb3-50ce05e9e6b9
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: ab05efc7baba58a34180faa038cb58c7f57f4af2
ms.contentlocale: zh-cn
ms.lasthandoff: 08/12/2017

---
# <a name="initializing-custom-assembly-objects"></a>初始化自定义程序集对象
  在某些情况下，您可能需要在实例化自定义程序集类中的属性值和字段值时初始化它们。 您最可能需要使用从报表的全局对象集合中提供给您的值来初始化自定义类。 执行此操作通过重写**OnInit**方法**代码**的报表的对象。 访问**OnInit**，使用**代码**报表定义的元素。 有两种技术来初始化属性或字段值中你打算在报表中使用的自定义程序集的类： 你可以声明并创建你的类使用的新实例**OnInit**，也可以调用公开的方法使用**OnInit**。  
  
## <a name="global-object-collections-and-initialization"></a>全局对象集合和初始化  
 若干集合可用于初始化您的自定义类变量。 你可以使用**Globals**和**用户**集合。 **参数**，**字段**和**ReportItems**集合不是可供你的报表生命周期中的点处时**OnInit**调用方法。 若要使用的共享的集合， **Globals**或**用户**，则需要包括**报表**对象引用。 例如，以初始化自定义类基于当前语言的用户访问报表，你**代码**元素可能如下所示：  
  
```  
<Code>  
   Dim m_myClass As MyClass  
  
   Protected Overrides Sub OnInit()  
      m_myClass = new MyClass(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 初始化上述类的属性值和字段值的一个方法就是声明您的类并通过调用某一覆盖的构造函数创建其新实例。  
  
 若要初始化你的自定义程序集中的类的属性和字段值的另一种方法是调用从定义公开可用方法**OnInit**方法。 您首先需要在报表定义文件中为您的类添加一个实例名称。 一旦添加了相应的程序集引用和实例名称后，可以调用您的初始化方法以初始化类的属性值和字段值。 你**OnInit**方法可能如下所示：  
  
```  
<Code>  
   Protected Overrides Sub OnInit()  
      m_myClass.MyInitializationMethod(Report.User!Language, _  
         Report.Globals!ExecutionTime)  
   End Sub  
</Code>  
```  
  
 有关添加自定义类程序集引用和实例名称的详细信息，请参阅[添加到报表 &#40; 程序集引用SSRS &#41;](../../reporting-services/report-design/add-an-assembly-reference-to-a-report-ssrs.md).  
  
 有关全局对象集合的详细信息，请参阅[表达式 &#40; 中的内置集合报表生成器和 SSRS &#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
## <a name="see-also"></a>另請參閱  
 [将自定义程序集用于报表](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
