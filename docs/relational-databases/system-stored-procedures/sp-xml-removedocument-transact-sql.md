---
title: sp_xml_removedocument （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xml_removedocument_TSQL
- sp_xml_removedocument
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xml_removedocument
ms.assetid: f9dca50a-8baf-4170-90bc-e72783ce5b73
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6219f18bee08d5c20431cb87a2cb30795c515d7a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67950475"
---
# <a name="sp_xml_removedocument-transact-sql"></a>sp_xml_removedocument (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  删除文档句柄指定的 XML 文档的内部表示形式并使该文档句柄无效。  
  
> [!NOTE]  
>  分析后的文档存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的内部缓存中。 MSXML 分析器 (Msxmlsql.dll) 占用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可用总内存的八分之一。 若要避免内存不足，请运行**sp_xml_removedocument**以释放内存。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_xml_removedocument hdoc  
```  
  
## <a name="arguments"></a>参数  
 *hdoc*  
 新建文档的句柄。 无效句柄将返回错误。 *hdoc*是一个整数。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 >0 （失败）  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="examples"></a>示例  
 以下示例删除 XML 文档的内部表示形式。 该文档的句柄作为输入提供。  
  
```  
EXEC sp_xml_removedocument @hdoc;  
```  
  
## <a name="see-also"></a>另请参阅      
 <br>[系统存储过程（Transact-sql）](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)
 <br>[XML 存储过程（Transact-sql）](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)
 <br>[sys. dm_exec_xml_handles （Transact-sql）](../system-dynamic-management-views/sys-dm-exec-xml-handles-transact-sql.md)
 <br>[sp_xml_preparedocument （Transact-sql）](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)
 <br>[OPENXML (Transact-SQL)](../../t-sql/functions/openxml-transact-sql.md)
  
  
