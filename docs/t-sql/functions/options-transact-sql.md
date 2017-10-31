---
title: "@@OPTIONS (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@OPTIONS'
- '@@OPTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, current SET options
- '@@OPTIONS function'
- current SET options
ms.assetid: 3d5c7f6e-157b-4231-bbb4-4645a11078b3
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 9480ffeffa83650b5cf44ad51547c36d5563b13b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40options-transact-sql"></a>&#x40;&#x40;选项 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回有关当前 SET 选项的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
@@OPTIONS  
```  
  
## <a name="return-types"></a>返回类型  
 **integer**  
  
## <a name="remarks"></a>注释  
 选项可以来自使用**设置**命令或从**sp_configure 用户选项**值。 使用配置的会话值**设置**命令替代**sp_configure**选项。 许多工具（例如 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 自动配置设置选项。 每个用户有 @@OPTIONS函数表示的配置。  
  
 可以使用 SET 语句更改特定用户会话的语言和查询处理选项。 **@@OPTIONS** 只能检测的选项设置为 ON 或 OFF。  
  
 **@@OPTIONS** 函数返回的选项，转换为基的 10 （十进制） 整数的位图。 位设置存储在主题中的表中描述的位置[配置用户选项，服务器配置选项](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)。  
  
 要解码**@@OPTIONS** 值时，请将返回整数转换**@@OPTIONS** 为二进制，然后查找在表上的值[配置用户选项，服务器配置选项](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)。 例如，如果`SELECT @@OPTIONS;`返回的值`5496`，使用 Windows 程序员计算器 (**calc.exe**) 若要将十进制转换`5496`为二进制。 结果为 `1010101111000`。 最右边的字符 （二进制 1、 2 和 4） 均为 0，指示表中的前三个项处于关闭状态。 咨询表，你看到这种**DISABLE_DEF_CNST_CHK**和**IMPLICIT_TRANSACTIONS**，和**CURSOR_CLOSE_ON_COMMIT**。 下一项 (**ANSI_WARNINGS**中`1000`位置) 上。 继续工作左但位图，和向下的选项列表中。 0 的最左侧的选项时，它们将被截断的类型转换。 位图 `1010101111000` 实际上是 `001010101111000`，代表全部 15 个选项。  
  
## <a name="examples"></a>示例  
  
### <a name="a-demonstration-of-how-changes-affect-behavior"></a>A. 更改如何影响行为的演示  
 下面的示例演示了两个不同设置的串联行为中的差异**CONCAT_NULL_YIELDS_NULL**选项。  
  
```  
SELECT @@OPTIONS AS OriginalOptionsValue;  
SET CONCAT_NULL_YIELDS_NULL OFF;  
SELECT 'abc' + NULL AS ResultWhen_OFF, @@OPTIONS AS OptionsValueWhen_OFF;  
  
SET CONCAT_NULL_YIELDS_NULL ON;  
SELECT 'abc' + NULL AS ResultWhen_ON, @@OPTIONS AS OptionsValueWhen_ON;  
```  
  
### <a name="b-testing-a-client-nocount-setting"></a>B. 测试客户端 NOCOUNT 设置  
 下面的示例设置`NOCOUNT``ON`，然后测试的值`@@OPTIONS`。 `NOCOUNT``ON`选项禁止有关被发送回请求客户端的会话中的每个语句影响的行数的消息。 `@@OPTIONS` 的值设置为 `512` (0x0200)。 这表示 NOCOUNT 选项。 下面的示例测试客户端是否启用了 NOCOUNT 选项。 例如，它可以帮助跟踪客户端的性能差异。  
  
```  
SET NOCOUNT ON  
IF @@OPTIONS & 512 > 0   
RAISERROR ('Current user has SET NOCOUNT turned on.', 1, 1)  
```  
  
## <a name="see-also"></a>另请参阅  
 [配置函数 (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [配置“用户选项”服务器配置选项](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)  
  
  

