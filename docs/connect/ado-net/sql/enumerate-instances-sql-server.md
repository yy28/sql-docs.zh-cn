---
title: 枚举 SQL Server 实例 (ADO.NET)
description: 介绍如何枚举 SQL Server 的活动实例。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ddf1c83c-9d40-45e6-b04d-9828c6cbbfdc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: bd0dbbedcb2fa33af80e0a1a1d593bf7df27edb6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896950"
---
# <a name="enumerating-instances-of-sql-server-adonet"></a>枚举 SQL Server 实例 (ADO.NET)

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server 允许应用程序在当前网络中查找 SQL Server 实例。 <xref:System.Data.Sql.SqlDataSourceEnumerator> 类向应用程序开发人员公开此信息，提供了包含所有可见服务器的相关信息的 <xref:System.Data.DataTable>。 此返回的表包含网络上可用服务器实例的列表（该列表与用户尝试创建新连接时提供的列表匹配），并展开“连接属性”对话框上包含所有可用服务器的下拉列表  。 显示的结果并不总是完整的。  
  
> [!NOTE]
>  与大多数 Windows 服务一样，最好以尽可能小的特权运行 SQL Browser 服务。 有关 SQL Browser 服务以及如何管理其行为的更多信息，请参见 SQL Server 联机丛书。  
  
## <a name="retrieving-an-enumerator-instance"></a>检索枚举器实例  
若要检索包含有关可用 SQL Server 实例的信息的表，必须先使用共享/静态 <xref:System.Data.Sql.SqlDataSourceEnumerator.Instance%2A> 属性来检索枚举器：  
  
```csharp  
System.Data.Sql.SqlDataSourceEnumerator instance =   
   System.Data.Sql.SqlDataSourceEnumerator.Instance  
```  
  
检索静态实例后，可以调用 <xref:System.Data.Sql.SqlDataSourceEnumerator.GetDataSources%2A> 方法，此方法返回包含可用服务器的相关信息的 <xref:System.Data.DataTable>：  
  
```csharp  
System.Data.DataTable dataTable = instance.GetDataSources();  
```  
  
通过方法调用返回的表包含以下列，其中所有列都包含 `string` 值：  
  
|列|说明|  
|------------|-----------------|  
|**ServerName**|服务器的名称。|  
|**InstanceName**|服务器实例的名称。 如果服务器作为默认实例运行，则为空。|  
|**IsClustered**|指明服务器是否属于群集。|  
|**版本**|服务器的版本。 例如：<br /><br /> -   9.00.x (SQL Server 2005)<br />-   10.0.xx (SQL Server 2008)<br />-   10.50.x (SQL Server 2008 R2)<br />-   11.0.xx (SQL Server 2012)|  
  
## <a name="enumeration-limitations"></a>枚举限制  
不一定会列出所有可用服务器。 此列表因超时和网络流量等因素而异。 这可能会导致两次连续调用生成不同的列表。 只有同一网络中的服务器才列出。 广播数据包通常不会遍历路由器，正因为此，可能看不到列出的服务器，但它跨调用是稳定的。  
  
列出的服务器不一定包含 `IsClustered` 和版本等其他信息。 这取决于列表的获取方式。 通过 SQL Server 浏览器服务列出的服务器比通过 Windows 基础结构发现的服务器具有更详细的信息，后者仅列出名称。  
  
> [!NOTE]
>  仅当在完全信任的环境中运行时，服务器枚举才可用。 在部分信任的环境中运行的程序集无法使用它，即使拥有 <xref:Microsoft.Data.SqlClient.SqlClientPermission> 代码访问安全性 (CAS) 权限，也不例外。  
  
SQL Server 通过使用名为 SQL Browser 的外部 Windows 服务来提供 <xref:System.Data.Sql.SqlDataSourceEnumerator> 的信息。 此服务默认处于启用状态，但管理员可以禁用它，让服务器实例对此类不可见。  
  
## <a name="example"></a>示例  
以下控制台应用程序检索所有可见 SQL Server 实例的信息，并在控制台窗口中显示该信息。  
  
```csharp  
using System.Data.Sql;  
  
class Program  
{  
  static void Main()  
  {  
    // Retrieve the enumerator instance and then the data.  
    SqlDataSourceEnumerator instance =  
      SqlDataSourceEnumerator.Instance;  
    System.Data.DataTable table = instance.GetDataSources();  
  
    // Display the contents of the table.  
    DisplayData(table);  
  
    Console.WriteLine("Press any key to continue.");  
    Console.ReadKey();  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
    foreach (System.Data.DataRow row in table.Rows)  
    {  
      foreach (System.Data.DataColumn col in table.Columns)  
      {  
        Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
      }  
      Console.WriteLine("============================");  
    }  
  }  
}  
```  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 和 ADO.NET](index.md)
