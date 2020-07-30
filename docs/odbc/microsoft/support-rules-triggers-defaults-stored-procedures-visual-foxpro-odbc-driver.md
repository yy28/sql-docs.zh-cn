---
title: 支持规则、触发器、默认值和存储过程 |Microsoft Docs
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
ms.openlocfilehash: a02aeea8f33e3a4d87fc771a7b0fa7b1a0067b6d
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363357"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>支持规则、触发器、默认值和存储过程（Visual FoxPro ODBC 驱动程序）
不能使用 Visual FoxPro ODBC 驱动程序创建视觉 FoxPro 规则、触发器、默认值或存储过程。 但是，当应用程序插入、更新或删除存储在数据库中的 Visual FoxPro 数据时，您的应用程序可能与现有规则、触发器、默认值或存储过程交互。  
  
 下表列出了规则、触发器、默认值或存储过程中的命令或函数时，Visual FoxPro ODBC 驱动程序支持的 Visual FoxPro 命令和函数。  
  
 如果您的应用程序与其规则、触发器、默认值或存储过程调用任何其他 Visual FoxPro 命令或函数的数据交互，则驱动程序将生成错误。 有关驱动程序不支持的命令和函数的列表，请参阅[不受支持的 Visual FoxPro 命令和函数](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md)。  
  
> [!TIP]  
>  如果要在规则、触发器或存储过程中插入条件代码，以确定驱动程序调用时要执行的命令，则可以使用**VERSION （）** 函数。 当驱动程序调用**VERSION （）** 函数时，该函数将返回 "VISUAL FoxPro ODBC 驱动程序 *\<version>* "。  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>规则、触发器、默认值和存储过程中支持的 Visual FoxPro 命令和函数  

:::row:::
    :::column:::
        $ 运算符  
        % 运算符  
    :::column-end:::
    :::column:::
        & 命令  
        && 命令  
    :::column-end:::
    :::column:::
        \* 命令  
        = 命令  
    :::column-end:::
:::row-end:::

## <a name="a"></a>A  

:::row:::
    :::column:::
        ABS （）函数  
        副本（）函数  
        ACOS （）函数  
        ADATABASES （）函数  
        ADBOBJECTS （）函数  
        添加表命令  
        ADEL （）函数  
        AELEMENT （）函数  
        AERROR （）函数  
        AFIELDS （）函数  
        AINS （）函数  
        ALEN （）函数  
        ALIAS （）函数  
    :::column-end:::
    :::column:::
        ALLTRIM （）函数  
        ALTER TABLE - SQL 命令  
        AND 运算符  
        追加命令  
        从命令追加  
        "从数组追加" 命令  
        追加常规命令  
        追加 MEMO 命令  
        追加过程命令  
        ASC （）函数  
        ASCAN （）函数  
        ASIN （）函数  
        ASORT （）函数  
    :::column-end:::
    :::column:::
        ASUBSCRIPT （）函数  
        AT （）函数  
        AT_C （）函数  
        ATAN （）函数  
        ATC （）函数  
        ATCC （）函数  
        ATCLINE （）函数  
        ATLINE （）函数  
        ATN2 （）函数  
        AUSED （）函数  
        AVERAGE 命令  
    :::column-end:::
:::row-end:::

## <a name="b"></a>B  

:::row:::
    :::column:::
        BEGIN TRANSACTION 命令  
        BETWEEN （）函数  
        BITAND （）函数  
        BITCLEAR （）函数  
        BITLSHIFT （）函数  
    :::column-end:::
    :::column:::
        BITNOT （）函数  
        BITOR （）函数  
        BITRSHIFT （）函数  
        位组（）函数  
        BITTEST （）函数  
    :::column-end:::
    :::column:::
        BITXOR （）函数  
        空白命令  
        BOF （）函数  
    :::column-end:::
:::row-end:::

## <a name="c"></a>C  

:::row:::
    :::column:::
        计算命令  
        候选（）函数  
        CDOW （）函数  
        CDX （）函数  
        天花板（）函数  
        CHR （）函数  
        CHRTRAN （）函数  
        CHRTRANC （）函数  
        关闭命令  
        CMONTH （）函数  
    :::column-end:::
    :::column:::
        继续命令  
        复制索引命令  
        复制过程命令  
        复制结构命令  
        复制结构扩展命令  
        COPY TAG 命令  
        复制到命令  
        复制到数组命令  
        COS （）函数  
        COUNT 命令  
    :::column-end:::
    :::column:::
        CPCONVERT （）函数  
        CPCURRENT （）函数  
        CPDBF （）函数  
        CTOD （）函数  
        CTOT （）函数  
        CURSORGETPROP （）函数  
        CURSORSETPROP （）函数  
        CURVAL （）函数  
    :::column-end:::
:::row-end:::

## <a name="d"></a>D  

:::row:::
    :::column:::
        DATE （）函数  
        DATETIME （）函数  
        DAY （）函数  
        DBC （）函数  
        DBF （）函数  
        DBGETPROP （）函数  
        DBUSED （）函数  
        DELETE - SQL 命令  
    :::column-end:::
    :::column:::
        删除命令  
        DELETE TAG 命令  
        DELETED （）函数  
        降序（）函数  
        差分（）函数  
        DIMENSION 命令  
        磁盘空间（）函数  
        DMY （）函数  
    :::column-end:::
    :::column:::
        DO 命令  
        DO CASE .。。ENDCASE 命令  
        ... .。。ENDDO 命令  
        DOW （）函数  
        DTOC （）函数  
        DTOR （）函数  
        DTO （）函数  
        DTOT （）函数  
    :::column-end:::
:::row-end:::

## <a name="e"></a>E  

:::row:::
    :::column:::
        EMPTY （）函数  
        END TRANSACTION 命令  
        EOF （）函数  
    :::column-end:::
    :::column:::
        ERROR （）函数  
        求值（）函数  
        EXIT 命令  
    :::column-end:::
    :::column:::
        EXP （）函数  
    :::column-end:::
:::row-end:::

## <a name="f"></a>F  

:::row:::
    :::column:::
        FCOUNT （）函数  
        FDATE （）函数  
        FIELD （）函数  
        FILE （）函数  
        FILTER （）函数  
        FLDLIST （）函数  
    :::column-end:::
    :::column:::
        FLOCK （）函数  
        FLOOR （）函数  
        FLUSH 命令  
        FOR （）函数  
        对于 .。。ENDFOR 命令  
        FOUND （）函数  
    :::column-end:::
    :::column:::
        自由表格命令  
        FSIZE （）函数  
        FTIME （）函数  
        FULLPATH （）函数  
        函数命令  
        FV （）函数  
    :::column-end:::
:::row-end:::

## <a name="g"></a>G  

:::row:::
    :::column:::
        收集命令  
        GETCP （）函数  
        GETENV （）函数  
    :::column-end:::
    :::column:::
        GETFLDSTATE （）函数  
        GETNEXTMODIFIED （）函数  
        中转/GOTO 命令  
    :::column-end:::
    :::column:::
        GOMONTH （）函数  
    :::column-end:::
:::row-end:::

## <a name="h"></a>H  

:::row:::
    :::column:::
        HEADER （）函数
    :::column-end:::
    :::column:::
        HOUR （）函数
    :::column-end:::
:::row-end:::

## <a name="i"></a>I  

:::row:::
    :::column:::
        IDXCOLLATE （）函数  
        IF .。。ENDIF 命令  
        IIF （）函数  
        INDBC （）函数  
        INDEX 命令  
        INLIST （）函数  
    :::column-end:::
    :::column:::
        INSERT-SQL 命令  
        INT （）函数  
        ISALPHA （）函数  
        ISBLANK （）函数  
        ISDIGIT （）函数  
        ISEXCLUSIVE （）函数  
    :::column-end:::
    :::column:::
        ISLEADBYTE （）函数  
        ISLOWER （）函数  
        ISNULL （）函数  
        ISREADONLY （）函数  
        ISUPPER （）函数  
    :::column-end:::
:::row-end:::

## <a name="k"></a>K  

:::row:::
    :::column:::
        KEY （）函数
    :::column-end:::
    :::column:::
        KEYMATCH （）函数
    :::column-end:::
:::row-end:::

## <a name="l"></a>L  

:::row:::
    :::column:::
        LEFT （）函数  
        LEFTC （）函数  
        LEN （）函数  
        LENC （）函数  
        LIKE （）函数  
        LIKEC （）函数  
    :::column-end:::
    :::column:::
        本地命令  
        定位命令  
        LOCK （）函数  
        LOG （）函数  
        LOG10 （）函数  
        LOOKUP （）函数  
    :::column-end:::
    :::column:::
        LOWER （）函数  
        LPARAMETERS 命令  
        LTRIM （）函数  
        LUPDATE （）函数  
    :::column-end:::
:::row-end:::

## <a name="m"></a>M  

:::row:::
    :::column:::
        MAX （）函数  
        MDX （）函数  
        MDY （）函数  
        MEMLINES （）函数  
    :::column-end:::
    :::column:::
        MESSAGE （）函数  
        MIN （）函数  
        MINUTE （）函数  
        _MLINE 系统内存变量  
    :::column-end:::
    :::column:::
        MLINE （）函数  
        MOD （）函数  
        MONTH （）函数  
        MTON （）函数  
    :::column-end:::
:::row-end:::

## <a name="n"></a>N  

:::row:::
    :::column:::
        NDX （）函数  
        正常化（）函数  
    :::column-end:::
    :::column:::
        NOT 运算符  
        NOTE 命令  
    :::column-end:::
    :::column:::
        NTOM （）函数  
        NVL （）函数  
    :::column-end:::
:::row-end:::

## <a name="o"></a>O  

:::row:::
    :::column:::
        发生（）函数  
        OLDVAL （）函数  
        ON （）函数  
    :::column-end:::
    :::column:::
        ON ERROR 命令  
        ON KEY 命令  
        打开数据库命令  
    :::column-end:::
    :::column:::
        OR 运算符  
        ORDER （）函数  
        OS （）函数  
    :::column-end:::
:::row-end:::

## <a name="p"></a>P  

:::row:::
    :::column:::
        PACK 命令  
        PADL （） &#124; PADR （） &#124; PADC （）函数  
        PARAMETERS 命令  
        PARAMETERS （）函数  
        支付（）函数  
    :::column-end:::
    :::column:::
        PI （）函数  
        PRIMARY （）函数  
        PRIVATE 命令  
        PROCEDURE 命令  
        PROGRAM （）函数  
    :::column-end:::
    :::column:::
        正确（）函数  
        PUBLIC 命令  
        PV （）函数  
    :::column-end:::
:::row-end:::

## <a name="r"></a>R  

:::row:::
    :::column:::
        RAND （）函数  
        RAT （）函数  
        RATC （）函数  
        RATLINE （）函数  
        撤回命令  
        RECCOUNT （）函数  
        RECNO （）函数  
        RECSIZE （）函数  
    :::column-end:::
    :::column:::
        区域命令  
        RELATION （）函数  
        删除表命令  
        REPLACE 命令  
        REPLACE FROM 数组命令  
        复制（）函数  
        重试命令  
        RETURN 命令  
    :::column-end:::
    :::column:::
        RIGHT （）函数  
        RIGHTC （）函数  
        RLOCK （）函数  
        ROLLBACK 命令  
        ROUND （）函数  
        RTOD （）函数  
        RTRIM （）函数  
    :::column-end:::
:::row-end:::

## <a name="s"></a>S  

:::row:::
    :::column:::
        扫描 .。。ENDSCAN 命令  
        散点命令  
        SEC （）函数  
        SECONDS （）函数  
        SEEK 命令  
        SEEK （）函数  
        选择命令  
        SELECT （）函数  
        SELECT-SQL 命令  
        SET （）函数  
        SET BLOCKSIZE 命令  
        设置命令  
        设置世纪命令  
        SET COLLATE 命令  
        "设置数据库" 命令  
        设置日期命令  
        设置默认命令  
        SET DELETED 命令  
        SET EXACT 命令  
        SET EXCLUSIVE 命令  
        SET FDOW 命令  
    :::column-end:::
    :::column:::
        设置字段命令  
        设置筛选器命令  
        设置固定命令  
        SET FULLPATH 命令  
        SET FWEEK 命令  
        设置时间命令  
        设置索引命令  
        设置 LOCK 命令  
        SET MULTILOCKS 命令  
        设置 NEAR 命令  
        SET NOCPTRANS 命令  
        设置通知命令  
        SET NULL 命令  
        设置优化命令  
        设置顺序命令  
        SET PATH 命令  
        设置过程命令  
        设置关系命令  
        设置关系关闭命令  
        SET REPROCESS 命令  
        SET SKIP 命令  
    :::column-end:::
    :::column:::
        SET UDFPARMS 命令  
        SET UNIQUE 命令  
        设置音量命令  
        SETFLDSTATE （）函数  
        SIGN （）函数  
        SIN （）函数  
        SKIP 命令  
        SORT 命令  
        SPACE （）函数  
        SQRT （）函数  
        存储命令  
        STR （）函数  
        STRCONV （）函数  
        STRTRAN （）函数  
        内容（）函数  
        STUFFC （）函数  
        SUBSTR （）函数  
        SUBSTRC （）函数  
        SUM 命令  
        SYS （2011）函数  
    :::column-end:::
:::row-end:::

## <a name="t"></a>T  

:::row:::
    :::column:::
        TABLEREVERT （）函数  
        TABLEUPDATE （）函数  
        TAG （）函数  
        TAGCOUNT （）函数  
        TAGNO （）函数  
        _TALLY 系统内存变量  
    :::column-end:::
    :::column:::
        TAN （）函数  
        TARGET （）函数  
        TIME （）函数  
        TOTAL 命令  
        _TRIGGERLEVEL 系统内存变量  
        TRIM （）函数  
    :::column-end:::
    :::column:::
        TTOC （）函数  
        TTOD （）函数  
        TXNLEVEL （）函数  
        TYPE （）函数  
    :::column-end:::
:::row-end:::

## <a name="u"></a>U  

:::row:::
    :::column:::
        UNIQUE （）函数  
        解除锁定命令  
        UPDATE 命令  
    :::column-end:::
    :::column:::
        UPDATE - SQL 命令  
        UPPER （）函数  
        USE 命令  
    :::column-end:::
    :::column:::
        USED （）函数  
    :::column-end:::
:::row-end:::

## <a name="v"></a>V  

:::row:::
    :::column:::
        VAL （）函数
    :::column-end:::
    :::column:::
        VERSION （）函数
    :::column-end:::
:::row-end:::

## <a name="w"></a>W  

WEEK （）函数

## <a name="y"></a>Y  

YEAR （）函数

## <a name="z"></a>Z  

ZAP 命令
