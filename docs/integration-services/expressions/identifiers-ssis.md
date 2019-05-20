---
title: 标识符 (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- regular identifiers [Integration Services]
- variables [Integration Services], expressions
- identifiers [Integration Services]
- expressions [Integration Services], variables
- lineage identifiers
- columns [Integration Services], identifiers
- names [Integration Services]
- expressions [Integration Services], identifiers
- qualified identifiers [Integration Services]
ms.assetid: 56af984d-88b4-4db8-b6a2-6b07315a699e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bd586c0ca3fa2cca354a2f394d9008761d744d41
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725366"
---
# <a name="identifiers-ssis"></a>标识符 (SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  在表达式中，标识符是可供运算使用的列和变量。 表达式可以使用常规标识符和限定标识符。  
  
## <a name="regular-identifiers"></a>常规标识符  
 常规标识符是不需要其他限定符的标识符。 例如， **MiddleName**（ **AdventureWorks** 数据库的 **Contacts** 表中的列）是常规标识符。  
  
 常规标识符的命名必须遵循以下这些规则：  
  
-   按照 Unicode 标准 2.0 的规定，名称的第一个字符必须是字母，或者是下划线“_”。  
  
-   后面的字符可以是在 Unicode 标准 2.0 中定义的字母或数字、下划线 (_) 以及字符 \@、$ 和 #。  
  
> [!IMPORTANT]  
>  常规标识符中不能包含空格和特殊字符（上述特殊字符除外）。 若要使用空格和特殊字符，必须使用限定标识符而不是常规标识符。  
  
## <a name="qualified-identifiers"></a>限定标识符  
 限定标识符是由方括号分隔的标识符。 标识符可能需要分隔符，因为标识符名称包括空格，或标识符名称不以字母或下划线字符开头。 例如，列名 **Middle Name** 必须由方括号限定，在表达式中书写为 [Middle Name]。  
  
 如果标识符的名称包含空格或名称不是有效的常规标识符名称，则必须对该标识符进行限定。 表达式计算器使用左右方括号 ([]) 来限定标识符。 方括号置于字符串的开头和末尾。 例如，标识符 5$> 将变为 [5$>]。 方括号可与列名、变量名和函数名一起使用。  
  
 如果使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器对话框生成表达式，则常规标识符将自动包含在方括号中。 但是，只有当名称包括无效字符时，才需要括号。 例如，名为 **MiddleName** 的列不带方括号也是有效的。  
  
 不能在表达式中引用包含方括号的列名。 例如，不能在表达式中使用列名 **Column[1]** 。 若要在表达式中使用此列，必须将其重命名为不带方括号的名称。  
  
## <a name="lineage-identifiers"></a>沿袭标识符  
 表达式可以使用沿袭标识符来引用列。 沿袭标识符是在首次创建包时自动分配的。 可以在 **设计器中** “高级编辑器” **对话框的** “列属性” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 选项卡上查看列的沿袭标识符。  
  
 如果使用列的沿袭标识符引用列，则标识符必须包含井号 (#) 字符前缀。 例如，必须将沿袭标识符为 147 的列引用为 #147。  
  
 如果表达式分析成功，则表达式计算器会将沿袭标识符替换为对话框中的列名。  
  
## <a name="unique-column-names"></a>唯一列名  
 包中使用的多个组件可能以相同的名称显示列。 如果在表达式中使用这些列，则必须消除它们的歧义后才能成功分析表达式。 表达式计算器支持用点分表示法标识列的源。 例如，两个名为 **Age** 的列可以成为 **FlatFileSource.Age** 和 **OLEDBSource.Age**，这表示它们的源分别是 FlatFileSource 和 OLEDBSource。 分析器将完全限定名视为单个列名。  
  
 源组件名和列名是分别限定的。 下列示例说明了点分表示法中方括号的有效用法：  
  
-   源组件名包含空格。  
  
    ```  
    [MySo urce].Age  
    ```  
  
-   列名的第一个字符无效。  
  
    ```  
    MySource.[#Age]  
    ```  
  
-   源组件名和列名包含无效字符。  
  
    ```  
    [MySource?].[#Age]  
    ```  
  
> [!IMPORTANT]  
>  如果点分表示法中的两个元素括在一对方括号中，则表达式计算器会将此元素对解释为单个标识符，而不是源-列组合。  
  
## <a name="variables-in-expressions"></a>表达式中的变量  
 表达式中引用的变量必须包含 \@ 前缀。 例如，使用 \@Counter 引用 Counter 变量。 \@ 字符不属于变量名，仅向表达式计算器指明标识符是变量。 如果使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器提供的对话框生成表达式，\@ 字符会自动添加到变量名中。 在 \@ 字符和变量名之间添加的空格无效。  
  
 变量名和其他常规标识符遵循同样的规则：  
  
-   按照 Unicode 标准 2.0 的规定，名称的第一个字符必须是字母，或者是下划线“_”。  
  
-   后面的字符可以是在 Unicode 标准 2.0 中定义的字母或数字、下划线 (_) 以及字符 \@、$ 和 #。  
  
 如果变量名中包含以上所列之外的字符，则必须将变量用方括号括起来。 例如，带有空格的变量名必须括在方括号内。 \@ 字符后面紧跟左括号。 例如，My Name 变量被引用为 \@[My Name]。 如果变量名和方括号间包含空格，则无效。  
  
> [!NOTE]  
>  用户定义的变量名和系统变量名区分大小写。  
  
## <a name="unique-variable-names"></a>唯一变量名  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 支持自定义变量并提供一组系统变量。 默认情况下，自定义变量属于 **User** 命名空间，而系统变量属于 **System** 命名空间。 可以为自定义变量创建其他命名空间并更新命名空间名称来满足应用程序要求。 表达式生成器列出了所有命名空间中的作用域内变量。  
  
 所有变量都有作用域并属于某个命名空间。 变量的作用域可以是包或者包中的容器或任务。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中的表达式生成器仅列出作用域内变量。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)和[在包中使用变量](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  
  
 表达式中使用的变量必须具有唯一的名称，表达式计算器才能正确地计算表达式。 如果包使用多个同名变量，则它们的命名空间必须不同。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供了命名空间解析运算符，该运算符由两个冒号 (::) 组成，用于以命名空间限定变量。 例如，下面的表达式使用两个名为 **Count**的变量；一个属于 **User** 命名空间，另一个属于 **MyNamespace** 命名空间。  
  
```  
@[User::Count] > @[MyNamespace::Count]  
```  
  
> [!IMPORTANT]  
>  必须将命名空间与限定的变量名二者的组合放在方括号中，表达式计算器才能识别该变量。  
  
 如果在 **User** 命名空间中 **Count** 的值是 10，而在 **MyNamespace** 中 **Count** 的值是 2，则表达式的计算结果是 **true** ，因为表达式计算器将它们识别为两个不同的变量。  
  
 如果变量名不唯一，将不会发生错误。 相反，表达式计算器将仅使用变量的一个实例来计算表达式并返回错误的结果。 例如，以下表达式原来是为了比较两个单独 **Count** 变量的值（10 和 2），但表达式的计算结果却是 **false** ，因为表达式计算器两次都使用了同一个 **Count** 变量实例。  
  
```  
@Count > @Count  
```  
  
## <a name="related-content"></a>相关内容  
 pragmaticworks.com 上的技术文章 [SSIS 表达式小抄表](https://go.microsoft.com/fwlink/?LinkId=746575)。  
  
  
