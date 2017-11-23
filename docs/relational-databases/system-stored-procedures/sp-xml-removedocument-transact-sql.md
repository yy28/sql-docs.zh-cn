---
title: "sp_xml_removedocument (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_xml_removedocument_TSQL
- sp_xml_removedocument
dev_langs: TSQL
helpviewer_keywords: sp_xml_removedocument
ms.assetid: f9dca50a-8baf-4170-90bc-e72783ce5b73
caps.latest.revision: "18"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 220431915e970460225d3b8b273a7943076c76b5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spxmlremovedocument-transact-sql"></a>sp_xml_removedocument (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除文档句柄指定的 XML 文档的内部表示形式并使该文档句柄无效。  
  
> [!NOTE]  
>  分析后的文档存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的内部缓存中。 MSXML 分析器 (Msxmlsql.dll) 占用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可用总内存的八分之一。 若要避免内存不足，运行**sp_xml_removedocument**若要释放的内存。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_xml_removedocument hdoc  
```  
  
## <a name="arguments"></a>参数  
 *hdoc*  
 新建文档的句柄。 无效句柄将返回错误。 *hdoc*是一个整数。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 >0（失败）  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 以下示例删除 XML 文档的内部表示形式。 该文档的句柄作为输入提供。  
  
```  
EXEC sp_xml_removedocument @hdoc;  
```  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [XML 存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)   
 [sp_xml_preparedocument (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)   
 [OPENXML (Transact-SQL)](../../t-sql/functions/openxml-transact-sql.md)  
  
  
