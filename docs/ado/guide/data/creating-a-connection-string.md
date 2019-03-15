---
title: 创建的连接字符串 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/20/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [ADO]
- connection strings [ADO]
ms.assetid: 14eae122-2d1e-40c8-b88e-b7cb8dfbc93b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 455fe1c3f5a19b498730909f1c56bf98b03ae51b
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2019
ms.locfileid: "57972766"
---
# <a name="creating-a-connection-string"></a>创建连接字符串
连接字符串包含用分号分隔的参数/值对 （即，参数） 的列表。 例如：  
  
```syntax
"arg1=val1; arg2=val2; ... argN=valN;"  
```  
  
 ADO 或指定的提供程序必须识别所有参数。  
  
 ADO 认识到连接字符串中的以下五个参数。  
  
|参数|Description|  
|--------------|-----------------|  
|*提供程序*|指定要用于连接的提供程序的名称。|  
|*文件名*|指定的特定于提供程序的文件 （例如，持久化的数据源对象） 包含预设的连接信息的名称。|  
|*URL*|连接字符串指定为标识资源，例如文件或目录的绝对 URL。|  
|*远程提供程序*|指定要打开客户端连接时使用的提供程序的名称。 （仅在远程数据服务中。）|  
|*远程服务器*|指定要打开客户端连接时使用的服务器的路径名称。 （仅在远程数据服务中。）|  
  
 其他参数传递给提供程序中名为*提供程序*参数，而无需通过 ADO 任何处理。  
  
 HelloData 应用程序中的[HelloData:一个简单的 ADO 应用程序](../../../ado/guide/data/hellodata-a-simple-ado-application.md)使用以下连接字符串：  
  
```vb
m_sConnStr = "Provider=SQLOLEDB;Data Source=MySqlServer;" & _  
             "Initial Catalog=Northwind;Integrated Security='SSPI';"  
```  
  
 在此连接字符串，ADO 仅识别`"Provider=SQLOLEDB"`参数，指定作为 ADO 数据源的 SQL Server 的 Microsoft OLE DB 访问接口。 其余的参数/值对， `"Data Source=MySqlServer; Initial Catalog=Northwind;Integrated Security='SSPI';"`，传递逐字字符串到此提供程序。 类型和此类参数的有效性是特定于提供程序。 有关可以在连接字符串中传递的有效参数的信息，请参阅单个提供程序的文档。  
  
 根据 OLE DB Provider for SQL Server 文档，您可以替换为"服务器"*数据源*参数和"数据库"，使*Initial Catalog*参数。 因此，以下连接字符串会生成与上面相同的结果：  
  
```vb
m_sConnStr = "Provider=SQLOLEDB;Server=MySqlServer;" & _  
             "Database=Northwind;Integrated Security='SSPI';"  
```
