---
title: 从文件中插入图像
description: 描述如何处理文件中的图像。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 35900aa2-5615-4174-8212-ba184c6b82fb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: d8f7b561a6aba4539964d73dacfd9e45db2dd6aa
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452177"
---
# <a name="inserting-an-image-from-a-file"></a>从文件中插入图像

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

您可以根据数据源中的字段类型，将二进制大型对象（BLOB）作为二进制或字符数据写入数据库。 BLOB 是指作为 `text`、`ntext` 和 `image` 数据类型的通用术语，通常包含文档和图片。  
  
若要将 BLOB 值写入数据库，请发出相应的 INSERT 或 UPDATE 语句并将 BLOB 值作为输入参数传递。 如果 BLOB 存储为文本（例如 SQL Server `text` 字段），则可以将 BLOB 作为字符串参数传递。 如果 BLOB 存储为二进制格式（例如 SQL Server `image` 字段），则可将 `byte` 类型的数组作为二进制参数传递。
  
## <a name="example"></a>示例  
下面的代码示例将员工信息添加到 Northwind 数据库的 Employees 表中。 将从文件中读取雇员照片，并将其添加到表中的 Photo 字段，这是一个图像字段。  
  
```csharp  
public static void AddEmployee(  
  string lastName,   
  string firstName,   
  string title,   
  DateTime hireDate,   
  int reportsTo,   
  string photoFilePath,   
  string connectionString)  
{  
  byte[] photo = GetPhoto(photoFilePath);  
  
  using (SqlConnection connection = new SqlConnection(  
    connectionString))  
  
  SqlCommand command = new SqlCommand(  
    "INSERT INTO Employees (LastName, FirstName, " +  
    "Title, HireDate, ReportsTo, Photo) " +  
    "Values(@LastName, @FirstName, @Title, " +  
    "@HireDate, @ReportsTo, @Photo)", connection);   
  
  command.Parameters.Add("@LastName",    
     SqlDbType.NVarChar, 20).Value = lastName;  
  command.Parameters.Add("@FirstName",   
      SqlDbType.NVarChar, 10).Value = firstName;  
  command.Parameters.Add("@Title",       
      SqlDbType.NVarChar, 30).Value = title;  
  command.Parameters.Add("@HireDate",   
       SqlDbType.DateTime).Value = hireDate;  
  command.Parameters.Add("@ReportsTo",   
      SqlDbType.Int).Value = reportsTo;  
  
  command.Parameters.Add("@Photo",  
      SqlDbType.Image, photo.Length).Value = photo;  
  
  connection.Open();  
  command.ExecuteNonQuery();  
  }  
}  
  
public static byte[] GetPhoto(string filePath)  
{  
  FileStream stream = new FileStream(  
      filePath, FileMode.Open, FileAccess.Read);  
  BinaryReader reader = new BinaryReader(stream);  
  
  byte[] photo = reader.ReadBytes((int)stream.Length);  
  
  reader.Close();  
  stream.Close();  
  
  return photo;  
}  
```  
  
## <a name="next-steps"></a>后续步骤
- [SQL Server 二进制和大值数据](sql-server-binary-large-value-data.md)
