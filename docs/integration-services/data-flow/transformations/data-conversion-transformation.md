---
title: 数据转换 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataconversiontrans.f1
- sql13.dts.designer.dataconversiontransformation.f1
helpviewer_keywords:
- converting data types [Integration Services]
- Data Conversion transformation
- data types [Integration Services], converting
ms.assetid: fd515bbc-6f49-4d0c-ae7f-6ea3c3f24a1c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e1573167bfe50e5dcb63734a90c7b9b5bd00e40a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297970"
---
# <a name="data-conversion-transformation"></a>数据转换

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  数据转换将输入列中的数据转换为其他数据类型，然后将其复制到新的输出列。 例如，包可从多个源中提取数据，然后用此转换将列转换为目标数据存储所需的数据类型。 可以对单个输入列应用多个转换。  
  
 使用此转换，包可以执行下列类型的数据转换：  
  
-   更改数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../../../integration-services/data-flow/integration-services-data-types.md)。  
  
    > [!NOTE]  
    >  如果将数据转换为日期或日期时间数据类型，则输出列中的日期为 ISO 格式，即使区域设置首选项指定了不同格式时也是如此。  
  
-   设置字符串数据的列长度和数值数据的精度及小数位数。 有关详细信息，请参阅[精度、小数位数和长度 (Transact-SQL)](../../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
-   指定一个代码页。 有关详细信息，请参阅 [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md)。  
  
    > [!NOTE]  
    >  在包含字符串数据类型的列之间复制时，两列必须使用相同的代码页。  
  
 如果字符串数据的输出列长度小于其对应的输入列长度，则输出数据将被截断。 有关详细信息，请参阅 [数据中的错误处理](../../../integration-services/data-flow/error-handling-in-data.md)。  
  
 此转换有一个输入、一个输出和一个错误输出。  
  
## <a name="related-tasks"></a>Related Tasks  
 可以通过 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。 有关在 SSIS 设计器中使用数据转换的信息，请参阅[使用数据转换将数据转换为其他数据类型](../../../integration-services/data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md)。 有关如何以编程方式设置此转换的属性的信息，请参阅 [通用属性](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796) 和 [转换自定义属性](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)。  
  
## <a name="related-content"></a>相关内容  
 blogs.msdn.com 上的博客文章 [SSIS 2008 中数据类型转换技术之间的性能比较](https://go.microsoft.com/fwlink/?LinkId=220823)。  
  
## <a name="data-conversion-transformation-editor"></a>数据转换编辑器
  可以使用 **“数据转换编辑器”** 对话框，选择要转换的列和要将列转换成的数据类型以及设置转换属性。  
  
> [!NOTE]  
>  数据转换的输出列的 **FastParse** 属性未在 **“数据转换编辑器”** 中提供，但可以使用 **“高级编辑器”** 进行设置。 有关此属性的详细信息，请参阅 [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)的“数据转换”部分。  
  
### <a name="options"></a>选项  
 **可用输入列**  
 使用复选框选择要转换的列。 选择后，会将输入列添加到下表中。  
  
 **输入列**  
 从可用输入列的列表中选择要转换的列。 通过选中上述相应的复选框即可选择输入列。  
  
 **输出别名**  
 为每一个新列键入一个别名。 默认为 **Copy of** 后接输入列名。不过，你也可以任选一个唯一的描述性名称。  
  
 **数据类型**  
 从列表中选择可用的数据类型。 有关详细信息，请参阅 [Integration Services 数据类型](../../../integration-services/data-flow/integration-services-data-types.md)。  
  
 **长度**  
 设置字符串数据的列长度。  
  
 **精度**  
 设置数字数据的精度。  
  
 **小数位数**  
 设置数字数据的小数位数。  
  
 **代码页**  
 为 DT_STR 类型的列选择相应的代码页。  
  
 **配置错误输出**  
 使用 [配置错误输出](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) 对话框指定处理行级错误的方式。  
  
## <a name="see-also"></a>另请参阅  
 [快速分析](https://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95)   
 [数据流](../../../integration-services/data-flow/data-flow.md)   
 [Integration Services 转换](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
