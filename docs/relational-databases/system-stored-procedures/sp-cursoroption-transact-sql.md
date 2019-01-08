---
title: sp_cursoroption (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursoroption_TSQL
- sp_cursoroption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoroption
ms.assetid: 88fc1dba-f4cb-47c0-92c2-bf398f4a382e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5a686f78ea5dff8a3ea551016d9fbe9c9046b110
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52545504"
---
# <a name="spcursoroption-transact-sql"></a>sp_cursoroption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  设置游标选项或返回由 sp_cursoropen 存储过程创建的游标信息。 sp_cursoroption 通过在表格格式数据流 (TDS) 包中指定 ID = 8 来调用。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_cursoroption cursor, code, value  
```  
  
## <a name="arguments"></a>参数  
 *cursor*  
 是*处理*生成的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]并由 sp_cursoropen 存储过程返回。 *游标*需要**int**输入值以用于执行。  
  
 *代码*  
 用于规定游标返回值的不同因素。 *代码*需要以下项之一**int**输入值：  
  
|ReplTest1|“属性”|Description|  
|-----------|----------|-----------------|  
|0x0001|TEXTPTR_ONLY|返回某些指定文本或图像列的文本指针，而非实际数据。<br /><br /> TEXTPTR_ONLY 允许将文本指针用作*句柄*blob 对象的更高版本可以有选择地检索或更新使用[!INCLUDE[tsql](../../includes/tsql-md.md)]或 DBLIB 工具 （例如[!INCLUDE[tsql](../../includes/tsql-md.md)] READTEXT 或 DBLIB DBWRITETEXT）。<br /><br /> 如果分配了值“0”，则选择列表中的所有文本和图像列将返回文本指针而非数据。|  
|0x0002|CURSOR_NAME|在指定的名称分配*值*到光标处。 这反过来允许 ODBC 使用[!INCLUDE[tsql](../../includes/tsql-md.md)]对通过 sp_cursoropen 打开的游标中定位的 UPDATE/DELETE 语句。<br /><br /> 可以将此字符串指定为任何字符或 Unicode 数据类型。<br /><br /> 由于[!INCLUDE[tsql](../../includes/tsql-md.md)]定位的 UPDATE/DELETE 语句操作，默认情况下，fat 游标中的第一行上 sp_cursor SETPOSITION 应该用于将光标放置在发出定位的 UPDATE/DELETE 语句之前。|  
|0x0003|TEXTDATA|为后续提取中的某些文本或图像列返回实际数据，而非文本指针（也即，此操作撤消了 TEXTPTR_ONLY 的效果）。<br /><br /> 如果为某特定列启用了 TEXTDATA，则将重新提取或刷新此行，然后将它发送回 TEXTPTR_ONLY。 借助于 TEXTPTR_ONLY，值参数是一个整数，它指定列编号，并且零值返回所有文本或图像列。|  
|0x0004|SCROLLOPT|滚动选项。 有关其他信息，请参阅本主题后面的“返回代码值”。|  
|0x0005|CCOPT|并发控制选项。 有关其他信息，请参阅本主题后面的“返回代码值”。|  
|0x0006|ROWCOUNT|结果集中的当前行数。<br /><br /> 注意：如果正在使用异步填充，则 ROWCOUNT 可能已由于 sp_cursoropen 返回的值而发生了变化。 如果行数未知，则返回值为-1。|  
  
 *value*  
 指定返回的值*代码*。 *值*是一个必需的参数，0x0001，0x0002，或 0x0003*代码*输入值。  
  
> [!NOTE]  
>  一个*代码*值 2 是字符串数据类型。 任何其他*代码*输入或返回的值*值*是一个整数。  
  
## <a name="return-code-values"></a>返回代码值  
 *值*参数可能会返回以下值之一*代码*值。  
  
|返回值|Description|  
|------------------|-----------------|  
|0x0004|SCROLLOPT|  
|0X0005|CCOPT|  
|0X0006|ROWCOUNT|  
  
 *值*参数返回以下 SCROLLOPT 值之一。  
  
|返回值|Description|  
|------------------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
  
 *值*参数返回以下 CCOPT 值之一。  
  
|返回值|Description|  
|------------------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS|  
|0x0004 或 0x0008|OPTIMISTIC|  
  
## <a name="see-also"></a>请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cursor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursor-transact-sql.md)   
 [sp_cursoropen &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)  
  
  
