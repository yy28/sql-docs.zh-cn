---
title: 步骤 3：使用 Node.js 连接到 SQL 的概念证明 | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5d5b41b6-129a-40b1-af8b-7e8fbd4a84bb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7dc49b466885e63ad9bd380a53a432a936310e18
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "68419255"
---
# <a name="step-3-proof-of-concept-connecting-to-sql-using-nodejs"></a>步骤 3：使用 Node.js 连接到 SQL 的概念证明

![Download-DownArrow-Circled](../../ssdt/media/download.png)[下载 Node.js SQL 驱动程序的具体步骤](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

应只将此示例视为概念证明。  为了清楚起见，此示例代码已经过简化，并不一定代表 Microsoft 建议的最佳做法。 Github 上提供了其他使用相同关键函数的示例：

- [https://github.com/tediousjs/tedious/blob/master/examples/](https://github.com/tediousjs/tedious/blob/master/examples/)
  
## <a name="step-1-connect"></a>步骤 1：连接  
  
new Connection 函数用于连接到 SQL 数据库。  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        server: 'your_server.database.windows.net',  //update me
        authentication: {
            type: 'default',
            options: {
                userName: 'your_username', //update me
                password: 'your_password'  //update me
            }
        },
        options: {
            // If you are on Microsoft Azure, you need encryption:
            encrypt: true,
            database: 'your_database'  //update me
        }
    };  
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
        // If no error, then good to proceed.
        console.log("Connected");  
    });  
```  
  
## <a name="step-2--execute-a-query"></a>步骤 2：执行查询  
  
  
所有 SQL 语句都是使用 new Request() 函数执行的。 如果语句返回了行（如 SELECT 语句），你可以使用 request.on() 函数检索这些行。 如果未返回行，request.on() 函数返回空列表。  
  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        server: 'your_server.database.windows.net',  //update me
        authentication: {
            type: 'default',
            options: {
                userName: 'your_username', //update me
                password: 'your_password'  //update me
            }
        },
        options: {
            // If you are on Microsoft Azure, you need encryption:
            encrypt: true,
            database: 'your_database'  //update me
        }
    }; 
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
        // If no error, then good to proceed.  
        console.log("Connected");  
        executeStatement();  
    });  
  
    var Request = require('tedious').Request;  
    var TYPES = require('tedious').TYPES;  
  
    function executeStatement() {  
        request = new Request("SELECT c.CustomerID, c.CompanyName,COUNT(soh.SalesOrderID) AS OrderCount FROM SalesLT.Customer AS c LEFT OUTER JOIN SalesLT.SalesOrderHeader AS soh ON c.CustomerID = soh.CustomerID GROUP BY c.CustomerID, c.CompanyName ORDER BY OrderCount DESC;", function(err) {  
        if (err) {  
            console.log(err);}  
        });  
        var result = "";  
        request.on('row', function(columns) {  
            columns.forEach(function(column) {  
              if (column.value === null) {  
                console.log('NULL');  
              } else {  
                result+= column.value + " ";  
              }  
            });  
            console.log(result);  
            result ="";  
        });  
  
        request.on('done', function(rowCount, more) {  
        console.log(rowCount + ' rows returned');  
        });  
        connection.execSql(request);  
    }  
```  
  
## <a name="step-3-insert-a-row"></a>步骤 3：插入行  
  
此示例展示了如何安全执行 [INSERT](../../t-sql/statements/insert-transact-sql.md) 语句，并传递用于保护应用程序免遭 [SQL 注入](../../relational-databases/tables/primary-and-foreign-key-constraints.md)值影响的参数。    
  
  
```javascript  
    var Connection = require('tedious').Connection;  
    var config = {  
        server: 'your_server.database.windows.net',  //update me
        authentication: {
            type: 'default',
            options: {
                userName: 'your_username', //update me
                password: 'your_password'  //update me
            }
        },
        options: {
            // If you are on Microsoft Azure, you need encryption:
            encrypt: true,
            database: 'your_database'  //update me
        }
    };  
    var connection = new Connection(config);  
    connection.on('connect', function(err) {  
        // If no error, then good to proceed.  
        console.log("Connected");  
        executeStatement1();  
    });  
  
    var Request = require('tedious').Request  
    var TYPES = require('tedious').TYPES;  
  
    function executeStatement1() {  
        request = new Request("INSERT SalesLT.Product (Name, ProductNumber, StandardCost, ListPrice, SellStartDate) OUTPUT INSERTED.ProductID VALUES (@Name, @Number, @Cost, @Price, CURRENT_TIMESTAMP);", function(err) {  
         if (err) {  
            console.log(err);}  
        });  
        request.addParameter('Name', TYPES.NVarChar,'SQL Server Express 2014');  
        request.addParameter('Number', TYPES.NVarChar , 'SQLEXPRESS2014');  
        request.addParameter('Cost', TYPES.Int, 11);  
        request.addParameter('Price', TYPES.Int,11);  
        request.on('row', function(columns) {  
            columns.forEach(function(column) {  
              if (column.value === null) {  
                console.log('NULL');  
              } else {  
                console.log("Product id of inserted item is " + column.value);  
              }  
            });  
        });       
        connection.execSql(request);  
    }  
```  
