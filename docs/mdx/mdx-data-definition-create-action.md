---
title: CREATE ACTION 语句 (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 762c2c1cc18d67ccafb05b0f61d213e5215de8b2
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34741286"
---
# <a name="mdx-data-definition---create-action"></a>MDX 数据定义的创建操作


  创建可以与多维数据集、维度、层次结构或从属对象关联的操作。  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE ACTION CURRENTCUBE | Cube_Name  
   .Action_Name <action body>  
<action body> ::=   
FOR   
        CUBE   
    | Hierarchy_Name [MEMBERS]   
    | Level_Name [MEMBERS]   
    | CELLS   
    | SET }   
      AS 'MDX_Expression'   
        [, TYPE = '  
              { URL   
            | HTML   
            | STATEMENT   
               | DATASET   
            | ROWSET   
            | COMMANDLINE   
               | PROPRIETARY }   
         ']  
   [ , INVOCATION = 'INTERACTIVE | ON_OPEN | BATCH ' ]  
   [ , APPLICATION = String_Expression ]  
   [ , DESCRIPTION = String_Expression ]  
   [ , CAPTION = 'MDX_Expression' ]  
```  
  
## <a name="arguments"></a>参数  
 *Cube_Name*  
 提供多维数据集名称的有效字符串。  
  
 *Action_ 名称*  
 一个提供所创建操作的名称的有效字符串。  
  
 *Hierarchy_ 名称*  
 一个提供层次结构名称的有效字符串。  
  
 *Level_ 名称*  
 一个提供级别名称的有效字符串。  
  
 *Member_ 名称*  
 一个提供成员名称或成员键的有效字符串。  
  
 *MDX_Expression*  
 有效的 MDX 表达式。  
  
 *String_Expression*  
 一个有效的字符串表达式。  
  
## <a name="remarks"></a>Remarks  
 客户端应用程序可能会创建和执行不安全的操作，也可能会使用不安全的函数。 若要避免这些情况下，使用**安全选项**属性。 有关详细信息，请参阅“Safety Options 属性”。  
  
> [!NOTE]  
>  包括此语句是为了向后兼容。 操作的新手[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，也不支持钻取或报表操作，如。  
  
## <a name="action-types"></a>操作类型  
 下表介绍中的可用操作的不同类型[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]。  
  
|操作类型|Description|  
|-----------------|-----------------|  
|**URL**|返回的操作字符串是一个 URL，应使用 Internet 浏览器打开此 URL。<br /><br /> 注意： 如果此操作不以开头`http://`或`https://`，该操作将向浏览器不可用除非**SafetyOptions**设置为**DBPROPVAL_MSMD_SAFETY_OPTIONS_ALLOW_ALL**。|  
|**HTML**|返回的操作字符串是一个 HTML 脚本。 应将该字符串保存到文件中，并使用 Internet 浏览器来呈现该文件。 在这种情况下，整个脚本会在所生成的 HTML 中运行。|  
|**语句**|返回的操作字符串是需要通过设置执行的语句**ICommand::SetText**命令对象与字符串和调用的方法**ICommand::Execute**方法。 如果该命令失败，会返回一条错误。|  
|**数据集**|返回的操作字符串是需要通过设置运行一个 MDX 语句**ICommand::SetText**命令对象与字符串和调用的方法**ICommand::Execute**方法。 所请求的接口 ID (IID) 应为**IDataset**。 如果创建了数据集，就说明命令成功了。 客户端应用程序应当允许用户浏览返回的数据集。|  
|**行集**|类似于**数据集**，但而不是请求的 IID **IDataset**，客户端应用程序应该要求的 IID **IRowset**。 如果创建了行集，就说明命令成功了。 客户端应用程序应当允许用户浏览返回的行集。|  
|**命令行**|客户端应用程序应执行该操作字符串。 该字符串是一个命令行。|  
|**专有**|客户端应用程序不应显示和执行该操作，除非该应用程序针对该操作进行了特殊的自定义设置。 专有操作不返回到客户端应用程序，除非客户端应用程序显式要求通过上设置适当的限制对它们进行**APPLICATION_NAME**。|  
  
## <a name="invocation-types"></a>调用类型  
 下表介绍了可在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中执行的各种调用。 调用类型仅用于帮助客户端应用程序来确定何时调用操作， 并不真正决定操作的调用行为。  
  
|调用类型|Description|  
|---------------------|-----------------|  
|**交互式**|应该由客户端应用程序通过用户交互来调用操作。|  
|**ON_OPEN**|应该在打开目标对象时由客户端应用程序调用操作。 目前尚未实现此调用类型。|  
|**批处理**|应该由客户端应用程序在某一批处理操作中涉及到目标对象（由客户端应用程序确定）时调用操作。 目前尚未实现此调用类型。|  
  
### <a name="scope"></a>范围  
 每个操作均针对一个特定的多维数据集定义，并且在该多维数据集中具有唯一的名称。 操作可具有下表所列的作用域之一。  
  
 多维数据集作用域  
 操作不依赖于特定的维度、成员或单元，例如：“为 AS/400 生产系统启动终端仿真”。  
  
 维度作用域  
 操作适用于特定的维度。 这些操作不依赖于所选的特定级别或成员。  
  
 级别作用域  
 操作适用于特定的维度级别。 这些操作不依赖于该维度中所选的特定成员。  
  
 成员作用域  
 操作适用于特定级别的成员。  
  
 单元作用域  
 操作仅适用于特定的单元。  
  
 集作用域  
 此操作仅适用于某个集。 该名称， **ActionParameterSet**，已保留供在操作的表达式内部应用程序。  
  
## <a name="see-also"></a>请参阅  
 [MDX 数据定义语句&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
