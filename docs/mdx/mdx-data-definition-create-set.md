---
title: 创建 SET 语句 (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- SET
- CREATE SET
- CREATE_SET
- CREATE
dev_langs:
- kbMDX
helpviewer_keywords:
- named sets [MDX]
- CREATE SET statement
ms.assetid: eff51eeb-5e7e-4706-b861-c57b6f3f89f0
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 0b7c9464085c99ff9d04be0c7c6a27d6f216c22b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---create-set"></a>MDX 数据定义-创建设置
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  为当前多维数据集创建具有会话作用域的命名集。  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE [SESSION] [ STATIC | DYNAMIC ] [HIDDEN] SET   
   CURRENTCUBE | Cube_Name  
      .Set_Name AS 'Set_Expression'  
      [,Property_Name = Property_Value, ...n]  
```  
  
## <a name="arguments"></a>参数  
 *Cube_Name*  
 有效的字符串表达式，它提供的多维数据集的名称。  
  
 *Set_Name*  
 为要创建的命名集提供名称的有效字符串表达式。  
  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *Property_Name*  
 提供集属性名称的有效字符串。  
  
 *Property_Value*  
 定义集属性值的有效标量表达式。  
  
## <a name="remarks"></a>注释  
 命名集是为重用而创建的维度成员集（或者是用于定义集的表达式）。 例如，使用命名集可以定义由销售额排在前十名的商店组成的维度成员集。 此组可以静态方式，或通过所示的函数定义[TopCount](../mdx/topcount-mdx.md)。 此命名集然后使用任何所需的一套前 10 个存储位置。  
  
 CREATE SET 语句创建命名的集，仍可在整个会话，并因此，可在多个查询在会话中。 有关详细信息，请参阅[Creating Session-Scoped 计算成员&#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md)。  
  
 也可以定义用于单个查询的命名集。 若要定义这种集，请在 SELECT 语句中使用 WITH 子句。 有关 WITH 子句的详细信息，请参阅[Creating Query-Scoped 命名集&#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets.md)。  
  
 *值赋*子句不能包含任何支持 MDX 语法的函数。 如果使用 CREATE SET 语句创建集时没有指定 SESSION 子句，则该集的作用域为会话。 使用 WITH 子句创建具有查询作用域的集。  
  
 指定当前连接的多维数据集以外的多维数据集将导致错误。 因此，应使用 CURRENTCUBE 来代替多维数据集名称，以表示当前的多维数据集。  
  
## <a name="scope"></a>范围  
 用户定义的集的作用域可以是下表所列的任意一个作用域。  
  
 查询作用域  
 集的可见性和生存期被限制在查询中。 集是在单个查询中定义的。 查询作用域将覆盖会话作用域。 有关详细信息，请参阅[Creating Query-Scoped 命名集&#40;MDX&#41;](../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets.md)。  
  
 会话作用域  
 集的可见性和生存期被限制在创建该集的会话中。 （如果对该集执行了 DROP SET 语句，集的生存期将短于会话的持续时间。）CREATE SET 语句创建的集的作用域为会话。 使用 WITH 子句创建具有查询作用域的集。  
  
### <a name="example"></a>示例  
 以下示例创建名为 Core Products 的集。 SELECT 查询并显示调用新创建的集。 必须先执行 CREATE SET 语句才可以执行 SELECT 查询 - 这两个语句不能在同一批中执行。  
  
```  
CREATE SET [Adventure Works].[Core Products] AS '{[Product].[Category].[Bikes]}'  
  
SELECT [Core Products] ON 0  
  FROM [Adventure Works]  
```  
  
## <a name="set-evaluation"></a>集的求取  
 集的求取可以定义不同的发生方式；可以定义为仅在集创建时发生一次，也可以定义为在每次使用集时发生。  
  
 STATIC  
 指示只在执行 CREATE SET 语句时，求取一次该集。  
  
 DYNAMIC  
 指示每次在查询中使用该集时，都进行求取。  
  
## <a name="set-visibility"></a>集的可见性  
 对于查询多维数据集的其他用户来说，集可以是可见的，也可以是不可见的。  
  
 HIDDEN  
 指定该集对查询多维数据集的用户不可见。  
  
## <a name="standard-properties"></a>标准属性  
 每个集都有一组默认属性。 当客户端应用程序连接到[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，默认属性为受支持，或可用于支持，如管理员将选择。  
  
|属性标识符|含义|  
|-------------------------|-------------|  
|CAPTION|客户端应用程序用作集标题的字符串。|  
|DISPLAY_FOLDER|标识客户端应用程序用来显示集的显示文件夹路径的字符串。 文件夹级别的分隔符由客户端应用程序定义。 有关工具和客户端提供[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，反斜杠 (\\) 是级别的分隔符。 若要为已定义的集提供多个显示文件夹，则使用分号 (;) 来分隔文件夹。|  
  
## <a name="see-also"></a>另请参阅  
 [拖放 SET 语句&#40;MDX&#41;](../mdx/mdx-data-definition-drop-set.md)   
 [MDX 数据定义语句&#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
