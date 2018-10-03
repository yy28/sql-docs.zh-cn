---
title: 映射 MySQL 和 SQL Server 字符设置 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: cebdf2ed28287a59ec9d4f0daaa1d0c200f8fe20
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47789025"
---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>映射 MySQL 和 SQL Server 字符集 (MySQLToSQL)
可以为 MySQL 字符数据类型、 表达式和文本指定字符集 (Charset)。  
  
## <a name="charset-mapping"></a>字符集映射  
字符集的映射是定义每个 MySQL 字符集，而在字符数据类型转换过程中使用。 它指定如何将特定字符集的字符串数据类型转换：  
  
-   为国家/地区的 SQL Server 字符类型 (NCHAR/NVARCHAR)，或  
  
-   到常规 SQL Server 字符类型 (CHAR/VARCHAR)  
  
1.  **国家/地区**目标数据库字符数据类型为：  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  **正则**目标数据库字符数据类型为：  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  类型映射仅允许映射到**国家/地区**字符数据类型。 根据类型映射转换 MySQL 字符数据类型后，将应用字符集的映射。  
  
> [!NOTE]  
> 字符集的映射可以在每个节点级别的元数据对象资源管理器上定义和表示从 MySQL 读取所有字符集。  
  
## <a name="charset-mapping-on-different-node-levels"></a>字符集映射上不同节点级别  
字符集映射各不相同在不同节点级别，即：  
  
1.  在根元数据节点级别  
  
2.  数据库、 类别和对象节点级别上  
  
> [!NOTE]  
> 为编辑字符集映射中，选择该选项卡包含三个按钮，而不考虑在不同节点级别上的映射。  
>   
> 它们分别是：  
>   
> 1.  **应用：** 适用的用户，仅当编辑，尚未保存字符集的映射时，才启用所做的更改。  
> 2.  **取消:** 取消用户所做的更改。 字符集的映射进行了编辑，但不是会保存时，获取启用该按钮。  
> 3.  **重置为默认值：** 重置为默认值的所有映射。  
  
1.  **在根元数据节点级别：** 字符集映射网格包含字符集网格具有每个字符集的单独列。 网格的列包括：  
  
    1.  名为网格的第一列**字符集名称**包含字符集名称。  
  
    2.  第二个名为**Charset 说明**包含字符集的说明。  
  
    3.  第三个列标题为**目标字符集类型**包含特定字符集映射设置。 此列的值有：  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
    > [!IMPORTANT]  
    > 特定字符集的默认值后 CHAR/VARCHAR 或 NCHAR/NVARCHAR 具有前缀 （默认）。  
  
    下面给出了 MySQL 数据库和根元数据节点级别上的目标数据库之间的字符集映射：  
  
    ||||  
    |-|-|-|  
    |**字符集名称**|**Charset 说明**|**目标字符集类型 （默认值）**|  
    |big5|Big5 中文 （繁体)|NCHAR/NVARCHAR （默认值）|  
    |dec8|DEC 西部欧洲|CHAR/VARCHAR （默认值）|  
    |cp850|DOS 西部欧洲|CHAR/VARCHAR （默认值）|  
    |hp8|HP 西部欧洲|CHAR/VARCHAR （默认值）|  
    |koi8r|KOI8-R Relcom 俄语|CHAR/VARCHAR （默认值）|  
    |拉丁语 1|cp1252 西部欧洲|CHAR/VARCHAR （默认值）|  
    |latin2|ISO 8859-2 中欧|CHAR/VARCHAR （默认值）|  
    |swe7|7 位瑞典语|CHAR/VARCHAR （默认值）|  
    |Ascii|US ASCII|CHAR/VARCHAR （默认值）|  
    |ujis|EUC-JP 日语|NCHAR/NVARCHAR （默认值）|  
    |sjis|Shift JIS 日语|NCHAR/NVARCHAR （默认值）|  
    |希伯来语|ISO 8859-8 希伯来语|CHAR/VARCHAR （默认值）|  
    |tis620|TIS620 泰语|CHAR/VARCHAR （默认值）|  
    |euckr|EUC-KR 朝鲜语|NCHAR/NVARCHAR （默认值）|  
    |koi8u|乌克兰语 KOI8-U|CHAR/VARCHAR （默认值）|  
    |gb2312|GB2312 简体中文|NCHAR/NVARCHAR （默认值）|  
    |希腊语|ISO 8859-7 希腊语|CHAR/VARCHAR （默认值）|  
    |cp 1250|Windows 中欧|CHAR/VARCHAR （默认值）|  
    |gbk|中文 （简体） GBK|NCHAR/NVARCHAR （默认值）|  
    |latin5|ISO 8859-9 土耳其语|CHAR/VARCHAR （默认值）|  
    |armscii8|ARMSCII 8 亚美尼亚语|CHAR/VARCHAR （默认值）|  
    |utf8|Utf-8 Unicode|NCHAR/NVARCHAR （默认值）|  
    |ucs2|Ucs-2 Unicode|NCHAR/NVARCHAR （默认值）|  
    |cp866|DOS 俄语|CHAR/VARCHAR （默认值）|  
    |keybcs2|DOS Kamenicky 捷克语斯洛伐克语|CHAR/VARCHAR （默认值）|  
    |macce|Mac 中欧|CHAR/VARCHAR （默认值）|  
    |macroman|Mac 西部欧洲|CHAR/VARCHAR （默认值）|  
    |cp852|DOS 中部欧洲|CHAR/VARCHAR （默认值）|  
    |latin7|ISO-8859 13 波罗的语|CHAR/VARCHAR （默认值）|  
    |cp 1251|Windows 西里尔文|CHAR/VARCHAR （默认值）|  
    |cp 1256|Windows 阿拉伯语|CHAR/VARCHAR （默认值）|  
    |cp 1257|Windows 波罗的语|CHAR/VARCHAR （默认值）|  
    |BINARY|二进制伪字符集|CHAR/VARCHAR （默认值）|  
    |geostd8|GEOSTD8 格鲁吉亚语|CHAR/VARCHAR （默认值）|  
    |cp932|Windows 日语 SJIS|NCHAR/NVARCHAR （默认值）|  
    |eucjpms|Windows 日语 UJIS|NCHAR/NVARCHAR （默认值）|  
  
2.  **在数据库、 类别或对象节点级别上：** 在数据库、 类别或对象节点级别中，字符集映射网格包含相同的行中的一个根元数据节点级别，报道。:  
  
    1.  标题为网格的第一列**字符设置名称**包含字符集名称。  
  
    2.  第二个列标题为**字符设置说明**包含字符集的说明。  
  
    3.  唯一的区别是该网格的第三个列中的值。 第三个列标题为**目标数据类型**包含特定字符集映射设置。 列的值有：  
  
        -   继承 （CHAR/VARCHAR 或 NCHAR/NVARCHAR）  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
> [!IMPORTANT]  
> -   在 MySQL 数据库和目标数据库上数据库、 类别和对象节点的层之间的字符集映射的默认值为根的列以外的其他每个级别上是特定字符集**目标数据类型**应为继承。  
> -   在网格中，值**继承**后缀与 '(CHAR/VARCHAR) 或 '(NCHAR/NVARCHAR) 具体取决于哪个值已从父项继承通过此特定字符集。  
  
