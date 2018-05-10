---
title: 比较字符串数据 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- comparing string data
- comparison options [Integration Services]
- locales [Integration Services]
- converting string data
- string comparisons
ms.assetid: 93aeb5bd-e208-46b7-8979-dea2dcd37d4c
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c60572c425df10ab659239217424d789bfe2abc1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="comparing-string-data"></a>比较字符串数据
  字符串比较是由 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]执行的许多转换中的重要组成部分，字符串比较也用在变量表达式和属性表达式的求值中。 例如，排序转换比较数据集中的值，从而以升序或降序对数据进行排序。  
  
## <a name="configuring-transformations-for-string-comparisons"></a>为字符串比较配置转换  
 可以自定义排序、聚合、模糊分组和模糊查找转换，以更改在列级比较字符串的方式。 例如，可以指定进行比较时忽略大小写，这意味着大写字符和小写字符将被视为相同的字符。  
  
 下列转换使用可以包含字符串比较的表达式。  
  
-   有条件拆分转换可以在表达式中使用字符串比较，以确定将数据行发送到哪个输出。 有关详细信息，请参阅 [Conditional Split Transformation](../../integration-services/data-flow/transformations/conditional-split-transformation.md)。  
  
-   派生列转换可以在表达式中使用字符串比较，以生成新的列值。 有关详细信息，请参阅 [Derived Column Transformation](../../integration-services/data-flow/transformations/derived-column-transformation.md)。  
  
 变量、变量映射和优先约束也使用可以包含字符串比较的表达式。 有关表达式的详细信息，请参阅 [Integration Services (SSIS) 表达式](../../integration-services/expressions/integration-services-ssis-expressions.md)。  
  
## <a name="processing-during-string-comparison"></a>字符串比较期间的处理  
 根据数据和转换的配置，在字符串数据比较的过程中可能需要进行下列处理：  
  
-   将数据转换为 Unicode 数据。 如果源数据尚不是 Unicode 数据，则自动将其转换为 Unicode 数据，然后开始比较。  
  
-   使用区域设置以应用区域设置特定的规则来解释日期、时间、十进制数据和排序顺序。  
  
-   在列级应用比较选项以更改比较敏感度。  
  
## <a name="converting-string-data-to-unicode"></a>将字符串数据转换为 Unicode 数据  
 根据转换执行的操作和转换的配置，字符串数据可能被转换为 DT_WSTR 数据类型，这是字符串字符的 Unicode 表示形式。  
  
 使用列的代码页可以将具有 DT_STR 数据类型的字符串数据转换为 Unicode 数据。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支持列级代码页，使用不同的代码页可以转换每个列。  
  
 在大多数情况下， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 可以从数据源中识别出正确的代码页。 例如，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，您可以在数据库和列级设置排序规则。 代码页从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序规则派生，这些规则可以是 Windows 排序规则或 SQL 排序规则。  
  
 如果 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供了意外的代码页，或包访问数据源时使用的访问接口未提供确定正确的代码页所需的足够信息，那么您可以在 OLE DB 源和 OLE DB 目标中指定一个默认代码页。 这样，在出现这种情况时将使用默认的代码页，而不使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的代码页。  
  
 文件没有代码页。 此时，包用来连接到文件数据的平面文件和多平面文件连接管理器，会包含一个用于指定文件的代码页的属性。 代码页只能在文件级设置，不能在列级设置。  
  
## <a name="setting-locale"></a>设置区域  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 不使用代码页来推断对数据排序或解释日期、时间和十进制数据时遵循的区域设置特定的规则。 相反，转换会读取在数据流组件、数据流任务、容器或包上的 LocaleId 属性所设置的区域设置。 默认情况下，转换从其数据流任务继承区域设置，而数据流任务又从包继承。 如果数据流任务位于像 For 循环容器这样的容器中，那么此数据流任务将从该容器中继承其区域设置。  
  
 还可以为平面文件连接管理器和多平面文件连接管理器指定区域设置。  
  
## <a name="setting-comparison-options"></a>设置比较选项  
 区域设置提供了比较字符串数据的基本规则。 例如，区域设置指定了字母表中每个字母的排序位置。 但是，当执行某些转换的比较时，这些规则可能还不够，不过， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支持一组比区域设置比较规则更详尽的高级比较选项。 这些比较选项在列级设置。 例如，利用这些比较选项之一，您可以忽略非空格字符。 此选项的作用是忽略标注字符，如重音符号，对比较来说， "a" 和 "á" 相同。  
  
 下表介绍比较选项和排序样式。  
  
|比较选项|Description|  
|-----------------------|-----------------|  
|忽略大小写|指定比较是否区分大小写字母。 如果设置了此选项，字符串比较会忽略大小写。 例如，"ABC" 和 "abc" 没有区别。|  
|忽略假名类型|指定比较是否区分日语的两种假名字符类型：平假名和片假名。 如果设置了此选项，字符串比较会忽略假名类型。|  
|忽略字符宽度|指定比较是否区分字符的单字节形式和该字符的双字节形式。 如果设置了此选项，字符串比较将把同一字符的单字节形式和双字节形式视为相同。|  
|忽略非空格字符|指定比较是否区分空格字符和标注字符。 如果设置了此选项，则比较会忽略标注字符。 例如，"å" 与 "a" 相同。|  
|忽略符号|指定比较是否区分字母字符和符号（如空格字符、标点、货币符号和数学符号）。 如果设置了此选项，字符串比较会忽略符号。 例如，" New York" 与 "New York" 相同，"*ABC" 与 "ABC"' 相同。|  
|将标点作为符号排序|指定比较是否对标点符号排序，并将除了连字符和撇号外的所有标点符号排在字母数字字符之前。 例如，如果设置了此选项，".ABC" 将会排在 "ABC" 前面。|  
  
 排序、聚合、模糊分组和模糊查找转换中包含了这些比较数据的选项。  
  
 **FullySensitive** 比较标志显示在模糊分组和模糊查找转换的 **“高级编辑器”** 对话框中。 选择 **FullySensitive** 比较标志意味着应用所有比较选项。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 数据类型](../../integration-services/data-flow/integration-services-data-types.md)   
 [快速分析](http://msdn.microsoft.com/library/6688707d-3c5b-404e-aa2f-e13092ac8d95)   
 [标准分析](http://msdn.microsoft.com/library/dfe835b1-ea52-4e18-a23a-5188c5b6f013)  
  
  
