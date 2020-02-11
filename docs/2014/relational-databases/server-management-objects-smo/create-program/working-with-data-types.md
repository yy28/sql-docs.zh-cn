---
title: 使用数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DataType object
- SQL Server Management Objects, data types
- data types [SMO]
- SMO [SQL Server], data types
ms.assetid: 1e0e736a-c709-4d89-aeb2-b32dcfd641fa
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d516901a3e44def9a0d6e19414bf0b972f9b37dc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63229084"
---
# <a name="working-with-data-types"></a>使用数据类型
  数据具有很多类型和不同的大小，例如具有定义长度的字符串、具有特定精度的数字或者作为具有其自身规则集的其他对象的用户定义数据类型。 <xref:Microsoft.SqlServer.Management.Smo.DataType>对象对数据类型进行分类，以便能够正确地[!INCLUDE[msCoName](../../../includes/msconame-md.md)]对其进行处理[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 
  <xref:Microsoft.SqlServer.Management.Smo.DataType> 对象与接受数据的对象关联。 以下 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理对象 (SMO) 接受必须由 <xref:Microsoft.SqlServer.Management.Smo.DataType> 对象属性定义的数据：  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Column>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedAggregateParameter>  
  
 可以通过若干方式设置接受数据的对象的 `DataType` 属性。  
  
-   使用默认构造函数，并显式指定 <xref:Microsoft.SqlServer.Management.Smo.DataType> 对象属性。  
  
-   使用重载的构造函数，并指定 <xref:Microsoft.SqlServer.Management.Smo.DataType> 属性作为参数。  
  
-   在对象构造函数中内联指定 <xref:Microsoft.SqlServer.Management.Smo.DataType>。  
  
-   使用 <xref:Microsoft.SqlServer.Management.Smo.DataType> 类的静态成员之一，例如 `Int`。 实际上，这将返回 <xref:Microsoft.SqlServer.Management.Smo.DataType> 对象的实例。  
  
 
  <xref:Microsoft.SqlServer.Management.Smo.DataType> 对象具有定义数据类型的几个属性。 例如，<xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 属性指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 枚举中列出了表示 <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 数据类型的常量值。 这是指诸如 `varchar`、`nchar`、`currency`、`integer`、`float` 和 `datetime` 这样的数据类型。  
  
 确立数据类型时，必须为数据设置具体的属性。 例如，如果它是 `nchar` 类型，则必须在 `Length` 属性中设置字符串数据的长度。 对数字值同样如此，这时必须指定精度和小数位数。  
  
 
  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> 和 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> 数据类型引用的对象包含由用户定义的数据类型的定义。 
  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> 基于来自 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 枚举的 <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 数据类型。 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>基于[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .net 数据类型。 通常，它们表示由于组织定义的业务规则而被数据库频繁重用的特定类型的数据。 例如，存储资金数量和货币币种的数据类型对于处理多种货币的公司将会非常有用。  
  
 
  <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> 枚举包含 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持的所有数据类型的列表。  
  
## <a name="examples"></a>示例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-basic"></a>使用 Visual Basic 中构造函数的规范构造 DataType 对象  
 该代码示例显示如何使用构造函数创建基于不同 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型的数据类型实例。  
  
> [!NOTE]  
>  
  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>、<xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> 和 XML 类型全都需要名称值以标识对象。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDataTypes1](SMO How to#SMO_VBDataTypes1)]  -->  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-c"></a>使用 Visual C# 中构造函数的规范构造 DataType 对象  
 该代码示例显示如何使用构造函数创建基于不同 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型的数据类型实例。  
  
> [!NOTE]  
>  
  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>、<xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> 和 XML 类型全都需要名称值以标识对象。  
  
```  
{   
//Declare a DataType object variable and define the data type in the constructor.   
DataType dt;   
//For the decimal data type the following two arguments specify precision, and scale.   
dt = new DataType(SqlDataType.Decimal, 10, 2);   
}  
```  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-basic"></a>使用 Visual Basic 中的默认构造函数构造 DataType 对象  
 该代码示例显示如何使用默认构造函数创建基于不同 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型的数据类型实例。 然后使用这些属性指定数据类型。  
  
 **注意**<xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>、 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>和 XML 类型都需要名称值以标识对象。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDataTypes2](SMO How to#SMO_VBDataTypes2)]  -->  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-c"></a>使用 Visual C# 中的默认构造函数构造 DataType 对象  
 该代码示例显示如何使用默认构造函数创建基于不同 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据类型的数据类型实例。 然后使用这些属性指定数据类型。  
  
 **注意**<xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>、 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>和 XML 类型都需要名称值以标识对象。  
  
```  
{   
//Declare and create a DataType object variable.   
DataType dt;   
dt = new DataType();   
//Define the data type by setting the SqlDataType property.   
dt.SqlDataType = SqlDataType.VarChar;   
//The VarChar data type requires a value for the MaximumLength property.   
dt.MaximumLength = 100;   
}  
```  
  
  
