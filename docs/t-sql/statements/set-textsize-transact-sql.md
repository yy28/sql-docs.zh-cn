---
title: "集 TEXTSIZE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 04/12/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TEXTSIZE_TSQL
- TEXTSIZE
- SET_TEXTSIZE_TSQL
- SET TEXTSIZE
dev_langs: TSQL
helpviewer_keywords:
- SET TEXTSIZE statement
- SELECT statement [SQL Server], text size returned
- size [SQL Server], text and image data
- TEXTSIZE option
- text size returned [SQL Server]
ms.assetid: 787154a6-39a6-4dd6-a6d0-67b4364f95d5
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5ecffd26c600d3a224824aa9a64ce347cd2f9fbc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="set-textsize-transact-sql"></a>SET TEXTSIZE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定的大小**varchar （max)**， **nvarchar (max)**， **varbinary （max)**，**文本**， **ntext**和**映像**SELECT 语句返回的数据。  
  
> [!IMPORTANT]  
>  **ntext**，**文本**，和**映像**的未来版本中将删除数据类型[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 请避免在新开发工作中使用这些数据类型，并考虑修改当前使用这些数据类型的应用程序。 请改用 **nvarchar(max)**、 **varchar(max)**和 **varbinary(max)** 。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
SET TEXTSIZE { number }   
```  
  
## <a name="arguments"></a>参数  
 *number*  
 长度是**varchar （max)**， **nvarchar (max)**， **varbinary （max)**，**文本**， **ntext**，或**映像**数据，以字节为单位。 *数*是最大值 2147483647 (2 GB) 的整数。  值-1 指示大小不受限制。 值为 0 将大小重置为默认值为 4 KB。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 （10.0 和更高版本） 和 ODBC Driver for[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自动指定`-1`时 （无限制） 连接。  
  
 **驱动程序早于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2008年:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口 （版本 9） 为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自动设置为 2147483647 TEXTSIZE，连接时。  
  
## <a name="remarks"></a>注释  
 设置将 SET TEXTSIZE 影响 @@TEXTSIZE函数。  
  
 SET TEXTSIZE 的设置是在执行或运行时设置的，而不是在分析时设置的。  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。  
  
## <a name="see-also"></a>另请参阅  
 [@@TEXTSIZE (Transact-SQL)](../../t-sql/functions/textsize-transact-sql.md)   
 [数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)   
 [SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
