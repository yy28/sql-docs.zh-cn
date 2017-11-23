---
title: "sp_cursoroption (Transact SQL) |Microsoft 文档"
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
- sp_cursoroption_TSQL
- sp_cursoroption
dev_langs: TSQL
helpviewer_keywords: sp_cursoroption
ms.assetid: 88fc1dba-f4cb-47c0-92c2-bf398f4a382e
caps.latest.revision: "8"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 247ab6fe3be339baca756d55c953021fe07683b7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spcursoroption-transact-sql"></a>sp_cursoroption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  设置游标选项或返回由 sp_cursoropen 存储过程创建的游标信息。 sp_cursoroption 通过在表格格式数据流 (TDS) 包中指定 ID = 8 来调用。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_cursoroption cursor, code, value  
```  
  
## <a name="arguments"></a>参数  
 *cursor*  
 是*处理*由生成的值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 sp_cursoropen 存储过程返回的。 *光标*需要**int**输入用于执行的值。  
  
 *代码*  
 用于规定游标返回值的不同因素。 *代码*需要以下项之一**int**输入值：  
  
|值|Name|Description|  
|-----------|----------|-----------------|  
|0x0001|TEXTPTR_ONLY|返回某些指定文本或图像列的文本指针，而非实际数据。<br /><br /> TEXTPTR_ONLY 允许文本指针用作*句柄*指向 blob 对象更高版本可以有选择地检索或更新使用[!INCLUDE[tsql](../../includes/tsql-md.md)]或 DBLIB 设施 （例如[!INCLUDE[tsql](../../includes/tsql-md.md)]READTEXT 或 DBLIB DBWRITETEXT）。<br /><br /> 如果分配了值“0”，则选择列表中的所有文本和图像列将返回文本指针而非数据。|  
|0x0002|CURSOR_NAME|将分配中指定的名称*值*到光标处。 这样，反过来，若要使用的 ODBC [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE/DELETE 语句位于通过 sp_cursoropen 打开的游标。<br /><br /> 可以将此字符串指定为任何字符或 Unicode 数据类型。<br /><br /> 由于[!INCLUDE[tsql](../../includes/tsql-md.md)]定位的更新/删除语句运行，默认情况下，在 fat 光标中的第一行上 sp_cursor SETPOSITION 应该用于将光标定位在颁发定位的 UPDATE/DELETE 语句之前。|  
|0x0003|TEXTDATA|为后续提取中的某些文本或图像列返回实际数据，而非文本指针（也即，此操作撤消了 TEXTPTR_ONLY 的效果）。<br /><br /> 如果为某特定列启用了 TEXTDATA，则将重新提取或刷新此行，然后将它发送回 TEXTPTR_ONLY。 借助于 TEXTPTR_ONLY，值参数是一个整数，它指定列编号，并且零值返回所有文本或图像列。|  
|0x0004|SCROLLOPT|滚动选项。 有关其他信息，请参阅本主题后面的“返回代码值”。|  
|0x0005|CCOPT|并发控制选项。 有关其他信息，请参阅本主题后面的“返回代码值”。|  
|0x0006|ROWCOUNT|结果集中的当前行数。<br /><br /> 注意： 行计数可能已更改自 sp_cursoropen 如果正在使用异步填充返回的值。 如果行数未知，则返回值 –1。|  
  
 *值*  
 指定返回的值*代码*。 *值*是必需的参数调用 0x0001、 0x0002，或 0x0003*代码*输入值。  
  
> [!NOTE]  
>  A*代码*的 2 的值是字符串数据类型。 任何其他*代码*输入或返回值*值*是一个整数。  
  
## <a name="return-code-values"></a>返回代码值  
 *值*参数可能会返回以下项之一*代码*值。  
  
|返回值|Description|  
|------------------|-----------------|  
|0x0004|SCROLLOPT|  
|0X0005|CCOPT|  
|0X0006|ROWCOUNT|  
  
 *值*参数将返回以下 SCROLLOPT 值之一。  
  
|返回值|Description|  
|------------------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
  
 *值*参数将返回以下 CCOPT 值之一。  
  
|返回值|Description|  
|------------------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS|  
|0x0004 或 0x0008|OPTIMISTIC|  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cursor &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursor-transact-sql.md)   
 [sp_cursoropen &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)  
  
  
