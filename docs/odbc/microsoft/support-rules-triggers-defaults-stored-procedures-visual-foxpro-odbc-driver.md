---
title: 对规则、 触发器、 默认值和存储的过程的支持 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], stored procedures
- FoxPro ODBC driver [ODBC], commands and functions
- commands for FoxPro ODBC driver [ODBC]
- FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], triggers
- stored procedures [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], rules
- FoxPro commands and functions [ODBC]
- rules [ODBC]
- Visual FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], rules
- functions [ODBC], Visual FoxPro
- default values [ODBC]
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro ODBC driver [ODBC], triggers
- FoxPro ODBC driver [ODBC], stored procedures
- Visual FoxPro commands and functions [ODBC]
ms.assetid: e449de20-d6ca-4902-9f8e-814eb6e86650
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 90a39ad540f3320ed78e981030679b59d911eeef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080776"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>支持规则、触发器、默认值和存储过程（Visual FoxPro ODBC 驱动程序）
无法创建 Visual FoxPro 规则、 触发器、 默认值或使用 Visual FoxPro ODBC 驱动程序的存储的过程。 但是，你的应用程序可能交互与现有规则、 触发器、 默认值或存储的过程中，因为它将插入、 更新或删除存储在数据库中的 Visual FoxPro 数据。  
  
 下表列出了 Visual FoxPro 命令和命令或函数中规则、 触发器、 默认值或存储的过程存在时，Visual FoxPro ODBC 驱动程序支持的函数。  
  
 如果应用程序与数据交互的规则、 触发器、 默认值，或存储的过程调用任何其他 Visual FoxPro 命令或函数，该驱动程序将生成错误。 请参阅[不受支持的 Visual FoxPro 命令和函数](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md)有关命令和驱动程序不支持的函数的列表。  
  
> [!TIP]  
>  如果你想要将条件代码插入到规则、 触发器或存储的过程，用于确定执行时调用的驱动程序的命令，则可以使用**版本 （)** 函数。 **版本 （)** 函数返回"Visual FoxPro ODBC 驱动程序 *\<版本 >* "驱动程序调用时。  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Visual FoxPro 命令和规则、 触发器、 默认值和存储的过程中支持的函数  
  
||||  
|-|-|-|  
|$ 运算符|%运算符|（& p) 命令|  
|& & 命令|* 命令|= 命令|  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|ABS （） 函数|副本 （） 函数|添加表命令|  
|ADATABASES （） 函数|ADBOBJECTS （） 函数|AERROR （） 函数|  
|ADEL （） 函数|AELEMENT （） 函数|ALEN （） 函数|  
|AFIELDS （） 函数|AINS （） 函数|ALTER TABLE - SQL 命令|  
|别名 （） 函数|ALLTRIM （） 函数|从数组命令追加|  
|AND 运算符|追加命令|追加备注命令|  
|追加命令|追加常规命令|ASCAN （） 函数|  
|追加过程命令|ASC （） 函数|ASUBSCRIPT （） 函数|  
|ASIN （） 函数|ASORT （） 函数|ATAN （） 函数|  
|在 （） 函数|AT_C （） 函数|ATCLINE （） 函数|  
|ATC （） 函数|ATCC （） 函数|AUSED （） 函数|  
|ATLINE （） 函数|ATN2 （） 函数||  
|平均命令|ACOS （） 函数||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|开始事务命令|之间 （） 函数|BITNOT （） 函数|  
|BITCLEAR （） 函数|BITLSHIFT （） 函数|位组 （） 函数|  
|BITOR （） 函数|BITRSHIFT （） 函数|空命令|  
|BITTEST （） 函数|BITXOR （） 函数||  
|BOF （） 函数|BITAND （） 函数||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|计算命令|候选 （） 函数|CHR （） 函数|  
|CDX （） 函数|CEILING （） 函数|关闭命令|  
|CHRTRAN （） 函数|CHRTRANC （） 函数|复制索引命令|  
|CMONTH （） 函数|继续命令|复制结构扩展命令|  
|复制过程命令|复制结构命令|将复制到命令|  
|复制标记命令|将复制到数组命令|CPCONVERT （） 函数|  
|COS （） 函数|将计数命令|CTOD （） 函数|  
|CPCURRENT （） 函数|CPDBF （） 函数|CURSORSETPROP （） 函数|  
|CTOT （） 函数|CURSORGETPROP （） 函数||  
|CURVAL （） 函数|CDOW （） 函数||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|DATE （） 函数|DATETIME （） 函数|DAY （） 函数|  
|DBC （） 函数|DBF （） 函数|DBGETPROP （） 函数|  
|DBUSED （） 函数|DELETE - SQL 命令|删除命令|  
|DELETE TAG 命令|已删除 （） 函数|降序 （） 函数|  
|DIFFERENCE （） 函数|维度命令|磁盘空间 （） 函数|  
|DMY （） 函数|执行用例...ENDCASE 命令|命令|  
|执行操作时...ENDDO 命令|DOW （） 函数|DTOC （） 函数|  
|DTOR （） 函数|DTO （） 函数|DTOT （） 函数|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|空 （） 函数|计算 （） 函数|退出命令|  
|错误 （） 函数|EXP （） 函数||  
|结束事务命令|EOF （） 函数||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|FCOUNT （） 函数|FDATE （） 函数|字段 （） 函数|  
|文件 （） 函数|筛选器 （） 函数|FLDLIST （） 函数|  
|纷纷采用 （） 函数|FLOOR （） 函数|刷新命令|  
|FOR...ENDFOR 命令|（） 函数|找到 （） 函数|  
|免费 TABLE 命令|FSIZE （） 函数|FTIME （） 函数|  
|FULLPATH （） 函数|函数命令|FV （） 函数|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|收集命令|GETNEXTMODIFIED （） 函数|转到/GOTO 命令|  
|GETFLDSTATE （） 函数|GOMONTH （） 函数||  
|GETCP （） 函数|GETENV （） 函数||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|标头 （） 函数|HOUR （） 函数|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IDXCOLLATE （） 函数|如果...ENDIF 命令|IIF （） 函数|  
|INDBC （） 函数|INDEX 命令|Inlist 的情况下 （） 函数|  
|插入 SQL 命令|INT （） 函数|ISALPHA （） 函数|  
|ISBLANK （） 函数|ISDIGIT （） 函数|ISEXCLUSIVE （） 函数|  
|ISLEADBYTE （） 函数|ISLOWER （） 函数|ISNULL （） 函数|  
|ISREADONLY （） 函数|ISUPPER （） 函数||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|钥匙 （） 函数|KEYMATCH （） 函数||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|左 （） 函数|LEFTC （） 函数|LIKEC （） 函数|  
|LENC （） 函数|类似于 （） 函数|LOCK （） 函数|  
|本地命令|查找命令|查找 （） 函数|  
|LOG （） 函数|LOG10 （） 函数|LTRIM （） 函数|  
|LOWER （） 函数|LPARAMETERS 命令||  
|LUPDATE （） 函数|LEN （） 函数||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|_MLINE 系统内存变量|MAX （） 函数|MDX （） 函数|  
|MDY （） 函数|MEMLINES （） 函数|消息 （） 函数|  
|MIN （） 函数|分钟 （） 函数|MLINE （） 函数|  
|MOD （） 函数|MONTH （） 函数|MTON （） 函数|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NDX （） 函数|规范化 （） 函数|NOT 运算符|  
|请注意命令|NTOM （） 函数|NVL （） 函数|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|发生 （） 函数|OLDVAL （） 函数|错误命令|  
|密钥命令|（） 函数|打开的数据库命令|  
|或运算符|ORDER （） 函数|OS （） 函数|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|PACK 命令|PARAMETERS （） 函数|付款 （） 函数|  
|参数命令|主 （） 函数|专用命令|  
|PI （） 函数|程序 （） 函数|正确的 （） 函数|  
|过程命令|PV （） 函数||  
|公共命令|PADL( ) &#124; PADR( ) &#124; PADC( ) Functions||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|RAND （） 函数|RAT （） 函数|RATC （） 函数|  
|RATLINE （） 函数|回想一下命令|RECCOUNT （） 函数|  
|RECNO （） 函数|RECSIZE （） 函数|区域命令|  
|关系 （） 函数|删除表命令|REPLACE 命令|  
|从数组命令替换|REPLICATE （） 函数|重试命令|  
|命令返回|右 （） 函数|RIGHTC （） 函数|  
|RLOCK （） 函数|ROLLBACK 命令|ROUND （） 函数|  
|RTOD （） 函数|RTRIM （） 函数||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|扫描...ENDSCAN 命令|命令的散点图|秒 （） 函数|  
|秒 （） 函数|查找命令|查找 （） 函数|  
|选择命令|选择 （） 函数|选择 SQL 命令|  
|SET BLOCKSIZE 命令|SET 携带命令|SET 世纪命令|  
|SET COLLATE 命令|设置数据库命令|设置日期命令|  
|设置默认命令|SET DELETED 命令|SET EXACT 命令|  
|SET EXCLUSIVE 命令|SET FDOW 命令|设置字段命令|  
|设置筛选器命令|设置固定的命令|SET FULLPATH 命令|  
|SET FWEEK 命令|设置的时间命令|设置索引命令|  
|SET LOCK 命令|SET MULTILOCKS 命令|附近命令设置|  
|SET NOCPTRANS 命令|设置通知命令|SET NULL 命令|  
|设置优化命令|SET 顺序命令|SET PATH 命令|  
|SET 过程命令|设置关系命令|设置关系关闭命令|  
|SET REPROCESS 命令|设置跳过命令|SET UDFPARMS 命令|  
|SET UNIQUE 命令|设置卷命令|SET （） 函数|  
|SETFLDSTATE （） 函数|SIGN （） 函数|SIN （） 函数|  
|跳过命令|排序命令|SPACE （） 函数|  
|SQRT （） 函数|存储命令|STR （） 函数|  
|STRCONV （） 函数|STRTRAN （） 函数|STUFF （） 函数|  
|STUFFC （） 函数|SUBSTR （） 函数|SUBSTRC （） 函数|  
|SUM 命令|SYS(2011) 函数||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TALLY 系统内存变量|_TRIGGERLEVEL 系统内存变量|TAGCOUNT （） 函数|  
|TABLEUPDATE （） 函数|标记 （） 函数|目标 （） 函数|  
|TAGNO （） 函数|TAN （） 函数|TRIM （） 函数|  
|时间 （） 函数|总命令|TXNLEVEL （） 函数|  
|TTOC （） 函数|TTOD （） 函数||  
|类型 （） 函数|TABLEREVERT （） 函数||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|唯一的 （） 函数|UNLOCK 命令|使用命令|  
|UPDATE 命令|上限 （） 函数||  
|使用 （） 函数|UPDATE - SQL 命令||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|VAL （） 函数|版本 （） 函数||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|一周 （） 函数|||  
  
## <a name="y"></a>Y  
  
||||  
|-|-|-|  
|YEAR （） 函数|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|ZAP 命令|||
