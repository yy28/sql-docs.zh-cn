---
title: SQL Server 排序规则名称 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- collations [SQL Server], SQL collations
- SQL collations
- names [SQL Server], collations
ms.assetid: 56483d24-add7-483d-9b96-c6fda460ddbc
caps.latest.revision: 30
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e3e03e3fec88d8d257c724bcfb44e1a1e7aa67f4
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43087008"
---
# <a name="sql-server-collation-name-transact-sql"></a>SQL Server 排序规则名称 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序规则指定排序规则名称的单个字符串。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持 Windows 排序规则。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 还支持有限数量（<80 个）的排序规则（称为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序规则），这些规则是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持的 Windows 排序规则之前开发的。 仍然支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序规则只是为了实现向后兼容性，不应将这些排序规则用于新开发工作。 有关 Windows 排序规则的详细信息，请参阅 [Windows 排序规则名称 (Transact-SQL)](../../t-sql/statements/windows-collation-name-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
<SQL_collation_name> :: =   
SQL_SortRules[_Pref]_CPCodepage_<ComparisonStyle>  
  
<ComparisonStyle> ::=  
_CaseSensitivity_AccentSensitivity | _BIN  
```  
  
## <a name="arguments"></a>参数  
 *SortRules*  
 标识字母表或语言的字符串，当指定按字典排序时应用该字母表或语言的排序规则。 例如 Latin1_General 或波兰语。  
  
 **Pref**  
 指定大写字母优先。 即使比较时不区分大小写，在没有其他区别的情况下，大写字母也将排在小写字母之前。  
  
 *Codepage*  
 指定用于标识排序规则所使用的代码页的 1 至 4 位数号码。 **CP1** 指定代码页 1252，对于其他所有代码页，则需指定完整的代码页编号。 例如，**CP1251** 指定代码页 1251，**CP850** 指定代码页 850。  
  
 CaseSensitivity  
 CI 指定不区分大小写，CS 指定区分大小写。  
  
 *AccentSensitivity*  
 AI 指定不区分重音，AS 指定区分重音。  
  
 **BIN**  
 指定使用二进制排序顺序。  
  
## <a name="remarks"></a>Remarks  
 若要列出您的服务器支持的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序规则，请执行以下查询。  
  
```  
SELECT * FROM sys.fn_helpcollations()   
WHERE name LIKE 'SQL%';  
```  

>  [!NOTE]  
>  对于排序顺序 ID 80，请使用代码页为 1250 的任何 Window 排序规则，并使用二进制顺序。 例如：Albanian_BIN、Croatian_BIN、Czech_BIN、Romanian_BIN、Slovak_BIN、Slovenian_BIN。  
  
## <a name="see-also"></a>另请参阅  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [常量 (Transact-SQL)](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-transact-sql.md?&tabs=sqlserver)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [表 (Transact-SQL)](../../t-sql/data-types/table-transact-sql.md)   
 [sys.fn_helpcollations (Transact-SQL)](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)  
  
  
