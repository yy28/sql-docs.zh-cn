---
title: CLR 集成自定义属性的概述 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- custom attributes [CLR integration]
- attributes [CLR integration]
- common language runtime [SQL Server], attributes
- database objects [CLR integration], custom attributes
- building database objects [CLR integration], custom attributes
ms.assetid: ecf5c097-0972-48e2-a9c0-b695b7dd2820
caps.latest.revision: 39
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2153277cbb0592b808fde3e0a8bec3a8ca582455
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37324937"
---
# <a name="overview-of-clr-integration-custom-attributes"></a>CLR 集成自定义属性的概览
  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 的公共语言运行时 (CLR) 允许使用称为属性的描述性关键字。 这些属性为许多元素（如方法和类）提供附加信息。 这些属性与对象的元数据一同保存在程序集中，并且可用于向其他开发工具描述您的代码，或者可用于影响 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内的运行时行为。  
  
 向 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 注册 CLR 例程时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将派生有关该例程的一组属性。 这些例程属性确定该例程的功能，包括是否可以对该例程编制索引。 例如，如果将 `DataAccess` 属性设置为 `DataAccessKind.Read`，您将能够访问 CLR 函数内的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户表中的数据。 下面的示例演示一个简单的示例中这`DataAccess`属性设置为了便于用户表中的数据访问**table1**。  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
  
public partial class UserDefinedFunctions  
{  
    [SqlFunction(DataAccess = DataAccessKind.Read)]  
    public static string func1()  
    {  
        // Open a connection and create a command  
        SqlConnection conn = new SqlConnection("context connection = true");  
        conn.Open();  
        SqlCommand cmd = conn.CreateCommand();  
        cmd.CommandText = "SELECT str_val FROM table1 WHERE int_val = 10";  
        // where table1 is a user table  
        // Execute this command   
        SqlDataReader rd = cmd.ExecuteReader();  
        // Set string ret_val to str_val returned from the query  
        string ret_val = rd.GetValue(0).ToString();  
        rd.Close();  
        return ret_val;  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Public partial Class UserDefinedFunctions  
    <SqlFunction(DataAccess = DataAccessKind.Read)> _   
    Public Shared Function func1() As String  
        ' Open a connection and create a command  
        Dim conn As SqlConnection = New SqlConnection("context connection = true")   
        conn.Open()  
        Dim cmd As SqlCommand =  conn.CreateCommand()   
        cmd.CommandText = "SELECT str_val FROM table1 WHERE int_val = 10"  
        ' where table1 is a user table  
        ' Execute this command   
        Dim rd As SqlDataReader =  cmd.ExecuteReader()   
        ' Set string ret_val to str_val returned from the query  
        Dim ret_val As String =  rd.GetValue(0).ToString()   
        rd.Close()  
        Return ret_val  
    End Function  
End Class  
```  
  
 对于 [!INCLUDE[tsql](../../includes/tsql-md.md)] 例程，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 从例程定义直接派生例程属性。 对于 CLR 例程，该服务器派生这些属性时并不分析例程主体； 您可以使用采用 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 语言实现的类和类成员的自定义属性。  
  
 在 `Microsoft.SqlServer.Server` 命名空间中定义 CLR 例程、用户定义类型和聚合所需的自定义属性。  
  
## <a name="see-also"></a>请参阅  
 [CLR 例程的自定义属性](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)  
  
  
