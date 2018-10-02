---
title: HOST_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- HOST_ID
- HOST_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IDs [SQL Server], workstations
- HOST_ID function
- workstation IDs [SQL Server]
- identification numbers [SQL Server], workstations
ms.assetid: 36ba56d4-20d7-4cd1-aa2a-e40a6c0a4e39
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c957a80753bb8f1be758a9af9f247e325de63490
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47728571"
---
# <a name="hostid-transact-sql"></a>HOST_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回工作站标识号。 工作站标识号是连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的客户端计算机上的应用程序的进程 ID (PID)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
HOST_ID ()  
```  
  
## <a name="return-types"></a>返回类型  
 **char(10)**  
  
## <a name="remarks"></a>Remarks  
 当该参数对系统函数可选时，则采用当前数据库、主机、服务器用户或数据库用户。 内置函数后面必须跟括号。  
  
 系统函数可以在选择列表、WHERE 子句和任何允许使用表达式的地方使用。  
  
## <a name="examples"></a>示例  
 以下示例创建一个表，该表在 `HOST_ID()` 定义中使用 `DEFAULT` 来记录那些向记录订单的表中插入行的计算机终端 ID。  
  
```  
CREATE TABLE Orders  
   (OrderID     int       PRIMARY KEY,  
    CustomerID  nchar(5)  REFERENCES Customers(CustomerID),  
    TerminalID  char(8)   NOT NULL DEFAULT HOST_ID(),  
    OrderDate   datetime  NOT NULL,  
    ShipDate    datetime  NULL,  
    ShipperID   int       NULL REFERENCES Shippers(ShipperID));  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [表达式 (Transact-SQL)](../../t-sql/language-elements/expressions-transact-sql.md)   
 [系统函数 (Transact-SQL)](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
