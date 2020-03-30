---
title: 从文件中插入图像
description: 介绍了如何处理文件中的图像。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 35900aa2-5615-4174-8212-ba184c6b82fb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 9d80f5eec2c33fed635c18937185e2e21798e93b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896724"
---
# <a name="inserting-an-image-from-a-file"></a>从文件中插入图像

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

可以将二进制大型对象 (BLOB) 作为二进制数据或字符数据（具体视数据源中的字段类型而定）写入数据库。 BLOB 这一通用术语是指，通常包含文档和图片的 `text`、`ntext` 和 `image` 数据类型。  
  
若要将 BLOB 值写入数据库，请发出相应的 INSERT 或 UPDATE 语句并将 BLOB 值作为输入参数传递。 如果 BLOB 存储为文本（如 SQL Server `text` 字段），可以将 BLOB 作为字符串参数传递。 如果 BLOB 以二进制格式存储（如 SQL Server `image` 字段），可以将 `byte` 类型的数组作为二进制参数传递。
  
## <a name="example"></a>示例  
下面的代码示例将员工信息添加到 Northwind 数据库中的 Employees 表。 它从文件中读取员工照片，并将它添加到表中的“照片”字段（图像字段）。  
  
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
