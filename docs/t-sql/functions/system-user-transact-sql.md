---
title: SYSTEM_USER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SYSTEM_USER_TSQL
- SYSTEM_USER
dev_langs:
- TSQL
helpviewer_keywords:
- current user names
- system-supplied user names [SQL Server]
- users [SQL Server], logins
- logins [SQL Server], identification name
- current system user names
- SYSTEM_USER function
- inserting system user name into table
- system usernames [SQL Server]
- users [SQL Server], names
ms.assetid: 565984cd-60c6-4df7-83ea-2349b838ccb2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 070e6a1b7d2e739b3f2b1f4c594ffdecd25fcb85
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="systemuser-transact-sql"></a>SYSTEM_USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  当未指定默认值时，允许将系统为当前登录名提供的值插入表中。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
SYSTEM_USER  
```  
  
## <a name="return-types"></a>返回类型  
 **nchar**  
  
## <a name="remarks"></a>Remarks  
 您可以在 CREATE TABLE 和 ALTER TABLE 语句中将 SYSTEM_USER 函数与 DEFAULT 约束一起使用。 还可以将此函数用作任意标准函数。  
  
 如果用户名与登录名不同，则 SYSTEM_USER 返回登录名。  
  
 如果当前用户使用 Windows 身份验证登录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则 SYSTEM_USER 返回如下形式的 Windows 登录标识名称：DOMAIN\\user_login_name。 但是，如果当前用户使用 SQL Server 身份验证登录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，则 SYSTEM_USER 返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录标识名称，例如为作为  `WillisJo` 登录的用户返回 `WillisJo`。  
  
 SYSTEM_USER 返回当前执行的上下文的名称。 如果已使用 EXECUTE AS 语句进行上下文切换，则 SYSTEM_USER 将返回模拟的上下文的名称。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-systemuser-to-return-the-current-system-user-name"></a>A. 使用 SYSTEM_USER 返回当前系统用户名  
 以下示例声明变量 `char`，在该变量中存储 `SYSTEM_USER` 的当前值，然后打印该变量中存储的值。  
  
```  
DECLARE @sys_usr char(30);  
SET @sys_usr = SYSTEM_USER;  
SELECT 'The current system user is: '+ @sys_usr;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
----------------------------------------------------------
The current system user is: WillisJo

(1 row(s) affected)
 ```  
  
### <a name="b-using-systemuser-with-default-constraints"></a>B. 将 SYSTEM_USER 与 DEFAULT 约束一起使用  
 以下示例创建一个表，其中 `SYSTEM_USER` 作为 `DEFAULT` 列的 `SRep_tracking_user` 约束。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE Sales.Sales_Tracking  
(  
    Territory_id int IDENTITY(2000, 1) NOT NULL,  
    Rep_id  int NOT NULL,  
    Last_sale datetime NOT NULL DEFAULT GETDATE(),  
    SRep_tracking_user varchar(30) NOT NULL DEFAULT SYSTEM_USER  
);  
GO  
INSERT Sales.Sales_Tracking (Rep_id)  
VALUES (151);  
INSERT Sales.Sales_Tracking (Rep_id, Last_sale)  
VALUES (293, '19980515');  
INSERT Sales.Sales_Tracking (Rep_id, Last_sale)  
VALUES (27882, '19980620');  
INSERT Sales.Sales_Tracking (Rep_id)  
VALUES (21392);  
INSERT Sales.Sales_Tracking (Rep_id, Last_sale)  
VALUES (24283, '19981130');  
GO  
```  
  
 以下查询选择 `Sales_Tracking` 表中的全部信息：  
  
```  
SELECT * FROM Sales_Tracking ORDER BY Rep_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
Territory_id Rep_id Last_sale            SRep_tracking_user
-----------  ------ -------------------- ------------------
2000         151    Mar 4 1998 10:36AM   ArvinDak
2001         293    May 15 1998 12:00AM  ArvinDak
2003         21392  Mar 4 1998 10:36AM   ArvinDak
2004         24283  Nov 3 1998 12:00AM   ArvinDak
2002         27882  Jun 20 1998 12:00AM  ArvinDak
  
(5 row(s) affected)
 ```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-systemuser-to-return-the-current-system-user-name"></a>C. 使用 SYSTEM_USER 返回当前系统用户名  
 以下示例返回 `SYSTEM_USER` 的当前值。  
  
```  
SELECT SYSTEM_USER;  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [CURRENT_TIMESTAMP (Transact-SQL)](../../t-sql/functions/current-timestamp-transact-sql.md)   
 [CURRENT_USER (Transact-SQL)](../../t-sql/functions/current-user-transact-sql.md)   
 [SESSION_USER (Transact-SQL)](../../t-sql/functions/session-user-transact-sql.md)   
 [System Functions (Transact-SQL)](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [USER (Transact-SQL)](../../t-sql/functions/user-transact-sql.md)  
  
  

