---
title: 操作数据
description: 收录了 MARS 应用程序编码示例。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 51096a2e-8b38-4c4d-a523-799bfdb7ec69
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 7855ef064061957cbc44dfcb4b075ebbd3893325
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247725"
---
# <a name="manipulating-data"></a>操作数据

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

在引入多重活动结果集 (MARS) 之前，开发人员必须使用多个连接或服务器端游标来解决某些情况。 此外，如果在事务情境下使用多个连接，则需要绑定的连接（使用 sp_getbindtoken 和 sp_bindsession）   。 以下场景说明了如何使用启用了 MARS 的连接，而不是使用多个连接。  
  
## <a name="using-multiple-commands-with-mars"></a>将多个命令与 MARS 结合使用  
下面的控制台应用程序演示如何使用两个包含两个 <xref:Microsoft.Data.SqlClient.SqlCommand> 对象的 <xref:Microsoft.Data.SqlClient.SqlDataReader> 对象和一个启用了 MARS 的 <xref:Microsoft.Data.SqlClient.SqlConnection> 对象。  
  
### <a name="example"></a>示例  
该示例将打开与 AdventureWorks  数据库的单个连接。 使用 <xref:Microsoft.Data.SqlClient.SqlCommand> 对象时，将创建一个 <xref:Microsoft.Data.SqlClient.SqlDataReader>。 使用阅读器时，打开第二个 <xref:Microsoft.Data.SqlClient.SqlDataReader>，使用第一个 <xref:Microsoft.Data.SqlClient.SqlDataReader> 的数据作为第二个阅读器的 WHERE 子句的输入。  
  
> [!NOTE]
>  下面的示例使用随 SQL Server 提供的 AdventureWorks 示例数据库  。 示例代码中提供的连接字符串假定数据库已安装并且在本地计算机上可用。 根据环境需要修改连接字符串。  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
class Class1  
{  
static void Main()  
{  
  // By default, MARS is disabled when connecting  
  // to a MARS-enabled host.  
  // It must be enabled in the connection string.  
  string connectionString = GetConnectionString();  
  
  int vendorID;  
  SqlDataReader productReader = null;  
  string vendorSQL =   
    "SELECT VendorId, Name FROM Purchasing.Vendor";  
  string productSQL =   
    "SELECT Production.Product.Name FROM Production.Product " +  
    "INNER JOIN Purchasing.ProductVendor " +  
    "ON Production.Product.ProductID = " +   
    "Purchasing.ProductVendor.ProductID " +  
    "WHERE Purchasing.ProductVendor.VendorID = @VendorId";  
  
  using (SqlConnection awConnection =   
    new SqlConnection(connectionString))  
  {  
    SqlCommand vendorCmd = new SqlCommand(vendorSQL, awConnection);  
    SqlCommand productCmd =   
      new SqlCommand(productSQL, awConnection);  
  
    productCmd.Parameters.Add("@VendorId", SqlDbType.Int);  
  
    awConnection.Open();  
    using (SqlDataReader vendorReader = vendorCmd.ExecuteReader())  
    {  
      while (vendorReader.Read())  
      {  
        Console.WriteLine(vendorReader["Name"]);  
  
        vendorID = (int)vendorReader["VendorId"];  
  
        productCmd.Parameters["@VendorId"].Value = vendorID;  
        // The following line of code requires  
        // a MARS-enabled connection.  
        productReader = productCmd.ExecuteReader();  
        using (productReader)  
        {  
          while (productReader.Read())  
          {  
            Console.WriteLine("  " +  
              productReader["Name"].ToString());  
          }  
        }  
      }  
  }  
      Console.WriteLine("Press any key to continue");  
      Console.ReadLine();  
    }  
  }  
  private static string GetConnectionString()  
  {  
    // To avoid storing the connection string in your code,  
    // you can retrieve it from a configuration file.  
    return "Data Source=(local);Integrated Security=SSPI;" +   
      "Initial Catalog=AdventureWorks;MultipleActiveResultSets=True";  
  }  
}  
```  
  
## <a name="reading-and-updating-data-with-mars"></a>用 MARS 读取和更新数据  
MARS 允许将连接用于读取操作和数据操作语言 (DML) 操作，其中有多个待处理操作。 此功能使应用程序无需处理连接繁忙错误。 此外，MARS 可以替换服务器端游标的用户，这通常会消耗更多资源。 最后，因为可以在单个连接上执行多个操作，所以，这些操作可以共享相同的事务上下文，不需要使用 sp_getbindtoken 和 sp_bindsession 系统存储过程   。  
  
### <a name="example"></a>示例  
下面的控制台应用程序演示如何使用两个包含三个 <xref:Microsoft.Data.SqlClient.SqlCommand> 对象的 <xref:Microsoft.Data.SqlClient.SqlDataReader> 对象和一个启用了 MARS 的 <xref:Microsoft.Data.SqlClient.SqlConnection> 对象。 第一个命令对象检索信用评级为 5 的供应商列表。 第二个命令对象使用 <xref:Microsoft.Data.SqlClient.SqlDataReader> 提供的供应商 ID 为第二个 <xref:Microsoft.Data.SqlClient.SqlDataReader> 加载特定供应商的所有产品。 每个产品记录由第二个 <xref:Microsoft.Data.SqlClient.SqlDataReader> 访问。 通过执行计算来确定新的 OnOrderQty  。 然后，通过第三个命令对象来使用新值更新 ProductVendor 表  。 整个过程发生在单个事务中，该事务在结束时回滚。  
  
> [!NOTE]
>  下面的示例使用随 SQL Server 提供的 AdventureWorks 示例数据库  。 示例代码中提供的连接字符串假定数据库已安装并且在本地计算机上可用。 根据环境需要修改连接字符串。  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
class Program  
{  
static void Main()  
{  
  // By default, MARS is disabled when connecting  
  // to a MARS-enabled host.  
  // It must be enabled in the connection string.  
  string connectionString = GetConnectionString();  
  
  SqlTransaction updateTx = null;  
  SqlCommand vendorCmd = null;  
  SqlCommand prodVendCmd = null;  
  SqlCommand updateCmd = null;  
  
  SqlDataReader prodVendReader = null;  
  
  int vendorID = 0;  
  int productID = 0;  
  int minOrderQty = 0;  
  int maxOrderQty = 0;  
  int onOrderQty = 0;  
  int recordsUpdated = 0;  
  int totalRecordsUpdated = 0;  
  
  string vendorSQL =  
      "SELECT VendorID, Name FROM Purchasing.Vendor " +   
      "WHERE CreditRating = 5";  
  string prodVendSQL =  
      "SELECT ProductID, MaxOrderQty, MinOrderQty, OnOrderQty " +  
      "FROM Purchasing.ProductVendor " +   
      "WHERE VendorID = @VendorID";  
  string updateSQL =  
      "UPDATE Purchasing.ProductVendor " +   
      "SET OnOrderQty = @OrderQty " +  
      "WHERE ProductID = @ProductID AND VendorID = @VendorID";  
  
  using (SqlConnection awConnection =   
    new SqlConnection(connectionString))  
  {  
    awConnection.Open();  
    updateTx = awConnection.BeginTransaction();  
  
    vendorCmd = new SqlCommand(vendorSQL, awConnection);  
    vendorCmd.Transaction = updateTx;  
  
    prodVendCmd = new SqlCommand(prodVendSQL, awConnection);  
    prodVendCmd.Transaction = updateTx;  
    prodVendCmd.Parameters.Add("@VendorId", SqlDbType.Int);  
  
    updateCmd = new SqlCommand(updateSQL, awConnection);  
    updateCmd.Transaction = updateTx;  
    updateCmd.Parameters.Add("@OrderQty", SqlDbType.Int);  
    updateCmd.Parameters.Add("@ProductID", SqlDbType.Int);  
    updateCmd.Parameters.Add("@VendorID", SqlDbType.Int);  
  
    using (SqlDataReader vendorReader = vendorCmd.ExecuteReader())  
    {  
      while (vendorReader.Read())  
      {  
        Console.WriteLine(vendorReader["Name"]);  
  
        vendorID = (int) vendorReader["VendorID"];  
        prodVendCmd.Parameters["@VendorID"].Value = vendorID;  
        prodVendReader = prodVendCmd.ExecuteReader();  
  
        using (prodVendReader)  
        {  
          while (prodVendReader.Read())  
          {  
            productID = (int) prodVendReader["ProductID"];  
  
            if (prodVendReader["OnOrderQty"] == DBNull.Value)  
            {  
              minOrderQty = (int) prodVendReader["MinOrderQty"];  
              onOrderQty = minOrderQty;  
            }  
            else  
            {  
              maxOrderQty = (int) prodVendReader["MaxOrderQty"];  
              onOrderQty = (int)(maxOrderQty / 2);  
            }  
  
            updateCmd.Parameters["@OrderQty"].Value = onOrderQty;  
            updateCmd.Parameters["@ProductID"].Value = productID;  
            updateCmd.Parameters["@VendorID"].Value = vendorID;  
  
            recordsUpdated = updateCmd.ExecuteNonQuery();  
            totalRecordsUpdated += recordsUpdated;  
          }  
        }  
      }  
    }  
    Console.WriteLine("Total Records Updated: " +   
      totalRecordsUpdated.ToString());  
    updateTx.Rollback();  
    Console.WriteLine("Transaction Rolled Back");  
  }  
  
  Console.WriteLine("Press any key to continue");  
  Console.ReadLine();  
}  
private static string GetConnectionString()  
{  
  // To avoid storing the connection string in your code,  
  // you can retrieve it from a configuration file.  
  return "Data Source=(local);Integrated Security=SSPI;" +   
    "Initial Catalog=AdventureWorks;" +   
    "MultipleActiveResultSets=True";  
  }  
}  
```  
  
## <a name="next-steps"></a>后续步骤
- [多重活动结果集 (MARS)](multiple-active-result-sets-mars.md)
