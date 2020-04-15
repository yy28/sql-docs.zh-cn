---
title: 支持规则、触发器、默认值和存储过程 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2fcf8e7c80b2712313cba81199489dc7cb06dce0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301134"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>支持规则、触发器、默认值和存储过程（Visual FoxPro ODBC 驱动程序）
无法使用 Visual FoxPro ODBC 驱动程序创建 Visual FoxPro 规则、触发器、默认值或存储过程。 但是，应用程序可能会在插入、更新或删除存储在数据库中的 Visual FoxPro 数据时与现有规则、触发器、默认值或存储过程进行交互。  
  
 下表列出了 Visual FoxPro ODBC 驱动程序支持的 Visual FoxPro 命令和函数，当命令或函数存在于规则、触发器、默认值或存储过程中时。  
  
 如果应用程序与规则、触发器、默认值或存储过程调用任何其他 Visual FoxPro 命令或函数的数据进行交互，则驱动程序将生成错误。 有关驱动程序不支持的命令和函数列表，请参阅[不支持的 Visual FoxPro 命令和函数](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md)列表。  
  
> [!TIP]  
>  如果要将条件代码插入到确定驱动程序调用时要执行的命令的规则、触发器或存储过程中，可以使用**VERSION（ ）** 函数。 当驱动程序调用时 **，VERSION（ ）** 函数返回"视觉 FoxPro ODBC 驱动程序*\<版本>"。 *  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>在规则、触发器、默认值和存储过程中支持可视化 FoxPro 命令和函数  
  
||||  
|-|-|-|  
|$ 运算符|% 运算符|&命令|  
|&& 指挥部|• 命令|• 命令|  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|ABS（ ） 功能|ACOPY） 功能|添加表命令|  
|ADATABASES（ ） 功能|ADBOBJECTS（ ） 功能|AERROR） 功能|  
|ADEL（ ） 功能|AELEMENT） 功能|放大缩小字体功能 放大缩小字体功能|  
|AFIELDS（ ） 功能|AINSS（ ） 功能|ALTER TABLE - SQL 命令|  
|ALIAS） 功能|ALLTRIM（ ） 功能|从 ARRAY 命令的附录|  
|和操作员|APPEND 命令|APPEND MEMO 命令|  
|从命令中应用|APPEND 总司令部|ASCANS 功能|  
|放大缩小字体功能 放大缩小字体功能|ASC（ ） 功能|放大缩小字体功能 放大缩小字体功能|  
|ASIN） 功能|ASORT） 功能|ATAN（ ） 功能|  
|AT（ ） 功能|AT_C（ ） 功能|ATCLINE（ ） 功能|  
|ATC（ ） 功能|ATCC（ ） 功能|AUSED） 功能|  
|ATline（ ） 功能|ATN2（ ） 功能||  
|平均命令|ACOS（ ） 功能||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|BEGIN 交易命令|（） 功能|BITNOT（ ） 功能|  
|BITCLEAR（ ） 功能|BITLSHIFT） 功能|BITSET） 功能|  
|BITOR（ ） 功能|BITRSHIFT） 功能|BLANK 命令|  
|BITTEST（ ） 功能|BITXOR（ ） 功能||  
|BOF（ ） 功能|BITand（ ） 功能||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|计算命令|候选人（ ） 功能|CHR（ ） 职能|  
|CDX（ ） 功能|天花板（ ） 功能|关闭命令|  
|CHRTRAN（ ） 功能|CHRTRANC（ ） 功能|复制索引命令|  
|CMONTH） 功能|继续命令|复制结构扩展命令|  
|复制程序命令|复制结构命令|复制到命令|  
|复制标签命令|复制到 ARRAY 命令|CPCONVERT） 功能|  
|COS（ ） 功能|COUNT 命令|CTOD（ ） 功能|  
|CPCURRENTS（ ） 功能|CPDBF（ ） 功能|放大缩小字体功能 放大缩小字体功能|  
|CTOT（ ） 功能|放大缩小字体功能 放大缩小字体功能||  
|曲线（ ） 功能|CDOW（ ） 功能||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|日期（ ） 功能|日期时间（ ） 功能|日（ ） 功能|  
|DBC（ ） 功能|DBF（ ） 功能|DBGETPROP（ ） 功能|  
|DBused（ ） 功能|DELETE - SQL 命令|删除命令|  
|DELETE TAG 命令|删除（ ） 功能|降序（ ） 功能|  
|差异（ ） 功能|维度命令|磁盘空间（ ） 功能|  
|DMY（ ） 功能|做案例...ENDCASE 命令|操作命令|  
|做， 而 ...ENDDO 命令|DOW（ ） 功能|DTOC（ ） 功能|  
|DTOR（ ） 功能|DTOS（ ） 功能|DTOT（ ） 功能|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|放大缩小字体功能 放大缩小字体功能|评估（ ） 功能|EXIT 命令|  
|错误（ ） 功能|EXP（ ） 功能||  
|结束交易命令|EOF（ ） 功能||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|FCOUNT（ ） 功能|FDATE） 功能|放大缩小字体功能 放大缩小字体功能|  
|文件（ ） 功能|过滤器（ ） 功能|FLDLIST（ ） 功能|  
|FLOCK（ ） 功能|地板（ ） 功能|FLUSH 命令|  
|对于 ...ENDFOR 命令|for（ ） 功能|FOUND（ ） 功能|  
|自由表命令|FSIZE（ ） 功能|FTIME（ ） 功能|  
|全路径（ ） 功能|职能命令|FV（ ） 功能|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|GATHER 命令|放大缩小字体功能 放大缩小字体功能|GO/GOTO 命令|  
|GETFLDSTATE（ ） 功能|GOmonth） 功能||  
|GETCP（ ） 功能|GETENV（ ） 功能||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|标题（ ） 功能|小时（ ） 功能|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IDXCOLLATE） 功能|如果。。。恩迪夫命令|IIF（ ） 功能|  
|INDBC（ ） 功能|INDEX 命令|INlist（ ） 功能|  
|插入 SQL 命令|INT（ ） 功能|ISALPHA（ ） 功能|  
|ISBLANK（ ） 功能|ISDigitS） 功能|是排他性（ ） 功能|  
|ISleadBY（ ） 功能|ISLOWER（ ） 功能|ISNULL（ ） 功能|  
|ISREAD） 功能|ISupper（ ） 功能||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|键（ ） 功能|键匹配（ ） 功能||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|左（ ） 功能|左撇子（ ） 功能|（完） 功能|  
|LENC（ ） 功能|喜欢） 功能|锁定 ） 功能|  
|本地命令|定位命令|查找（ ） 功能|  
|日志（ ） 功能|LOG10（ ） 功能|LTRIM（ ） 功能|  
|低（） 功能|LPARAMETERS 命令||  
|放大缩小字体功能 放大缩小字体功能|LEN（ ） 功能||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|_MLINE系统内存变量|最大（） 功能|MDX（ ） 功能|  
|MDY（ ） 功能|MEMLINES（ ） 功能|消息（ ） 功能|  
|最小值 ） 功能|分钟（ ） 功能|MLINE（ ） 功能|  
|MOD（ ） 功能|月（ ） 功能|MTONS ） 功能|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NDX（ ） 功能|放大缩小字体功能 放大缩小字体功能|不是操作员|  
|注释命令|NTOM（ ） 功能|NVL（ ） 功能|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|发生（ ） 功能|旧瓦尔（ ） 功能|上错误命令|  
|在关键命令|打开（ ） 功能|打开数据库命令|  
|或操作员|订单（ ） 功能|操作系统（ ） 功能|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|PACK 命令|参数（ ） 功能|付款（ ） 功能|  
|参数命令|初级功能|私人命令|  
|PI（ ） 功能|程序（ ） 功能|正（ ） 功能|  
|程序命令|PV（ ） 功能||  
|公共命令|PADL（ ） &#124; PADR（ ） &#124; PADC （ ） 功能||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|兰德（ ） 功能|RAT（ ） 功能|RATC（ ） 功能|  
|RATLINE（ ） 功能|RECALL 命令|（完） 功能|  
|RECNO（ ） 功能|放大缩小字体功能 放大缩小字体功能|区域司令部|  
|关系（ ） 功能|删除 TABLE 命令|替换命令|  
|从 ARRAY 命令替换|复制（ ） 功能|RETRY 命令|  
|返回命令|右） 功能|右C（ ） 功能|  
|RLOCK（ ） 功能|回滚命令|ROUND（ ） 功能|  
|RTOD（ ） 功能|RTRIM（ ） 功能||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|扫描。。。ENDSCAN 命令|分散命令|SEC（ ） 功能|  
|放大缩小字体功能 放大缩小字体功能|SEEK 命令|服务（ ） 功能|  
|选择命令|选择（ ） 功能|SELECT-SQL 命令|  
|SET BLOCKSIZE 命令|SET CARRY 命令|设置世纪命令|  
|SET COLLATE 命令|设置数据库命令|SET 日期命令|  
|设置默认命令|SET DELETED 命令|SET EXACT 命令|  
|SET EXCLUSIVE 命令|SET FDOW 命令|SET FIELDS 命令|  
|设置筛选器命令|设置固定命令|设置全PATH命令|  
|SET FWEEK 命令|SETHOURS 命令|SET INDEX 命令|  
|设置锁定命令|设置多锁命令|设置近命令|  
|设置 NOCPTRANS 命令|设置通知命令|SET NULL 命令|  
|设置优化命令|SET ORDER 命令|SET PATH 命令|  
|设置程序命令|设置关系命令|设置关系关闭命令|  
|SET REPROCESS 命令|SET SKIP 命令|SET UDFPARMS 命令|  
|SET UNIQUE 命令|SET VOLUME 命令|设置） 功能|  
|SETFLDSTATE（ ） 功能|符号 （ ） 功能|SINS ） 功能|  
|SKIP 命令|SORT 命令|空格（ ） 功能|  
|SQRT（ ） 功能|存储命令|STR（ ） 功能|  
|STRCONV（ ） 功能|放大缩小字体功能 放大缩小字体功能|STUFF（ ） 功能|  
|STUFFC（ ） 功能|SUBSTR（ ） 功能|SUBSTRC（ ） 功能|  
|SUM 命令|SYS（2011）功能||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TALLY系统内存变量|_TRIGGERLEVEL系统内存变量|标签计数（ ） 功能|  
|表更新（ ） 功能|标记（ ） 功能|目标（ ） 功能|  
|TAGNO（ ） 功能|TAN（ ） 功能|修剪 （ ） 功能|  
|时间（ ） 功能|总命令|TXNLEVEL（ ） 功能|  
|TTOC（ ） 功能|TTOD（ ） 功能||  
|类型（ ） 功能|表还原（ ） 功能||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|唯一功能|UNLOCK 命令|使用命令|  
|更新命令|上部（ ） 功能||  
|已用 （ ） 功能|UPDATE - SQL 命令||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|VAL（ ） 功能|版本（ ） 功能||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|周（ ） 功能|||  
  
## <a name="y"></a>Y  
  
||||  
|-|-|-|  
|年（ ） 功能|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|ZAP 命令|||
