---
title: 将 MySQL 和 SQL Server 字符映射设置 (MySQLToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 0a0b1abc184a6c7c0031d1b8d2dacd6d05cda324
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>将 MySQL 和 SQL Server 字符映射设置 (MySQLToSQL)
可以为 MySQL 字符数据类型、 表达式和文本指定字符集 （字符集）。  
  
## <a name="charset-mapping"></a>字符集映射  
字符集的映射是为每个 MySQL charset 定义，使用字符数据类型转换的过程。 它指定如何将转换的特定字符集的字符字符串数据类型：  
  
-   到 SQL Server 的国家/地区字符类型 (NCHAR/NVARCHAR)，或  
  
-   到常规 SQL Server 的字符类型 (CHAR/VARCHAR)  
  
1.  **国家/地区**目标数据库字符数据类型是：  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  **正则**目标数据库字符数据类型是：  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  类型映射仅允许映射到**国家/地区**字符数据类型。 MySQL 字符数据类型转换按照类型映射后，将应用字符集的映射。  
  
> [!NOTE]  
> 字符集映射可以在每个节点级别的元数据对象资源管理器上定义并表示从 MySQL 读取的所有字符集。  
  
## <a name="charset-mapping-on-different-node-levels"></a>字符集映射不同节点级别  
字符集映射而异不同节点级别，即：  
  
1.  在根元数据节点级别上  
  
2.  在数据库、 类别和对象节点级别上  
  
> [!NOTE]  
> 为编辑 Charset 映射中，选择该选项卡包含三个按钮，而不考虑的不同节点级别的映射。  
>   
> 它们分别是：  
>   
> 1.  **应用：**应用用户，仅当字符集的映射进行编辑，尚未保存时，才启用所做的更改。  
> 2.  **取消:** 取消用户所做的更改。 字符集的映射进行了编辑，但不是会保存时，获取启用该按钮。  
> 3.  **重置为默认值：**将所有映射重都置为默认值。  
  
1.  **在根元数据节点级别：** Charset 映射网格包含 charset 网格与每个字符集为一个单独的列。 网格中的列是：  
  
    1.  名为网格的第一列**Charset 名称**包含字符集名称。  
  
    2.  第二个名为**Charset 说明**包含 charset 说明。  
  
    3.  第三列的标题，**字符集类型，目标**包含特定的字符集的映射设置。 此列的值有：  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
    > [!IMPORTANT]  
    > 特定的字符集的默认值之后 CHAR/VARCHAR 或 NCHAR/NVARCHAR 具有前缀 （默认）。  
  
    MySQL 数据库和根元数据节点级别上的目标数据库之间的字符集映射如下所示：  
  
    ||||  
    |-|-|-|  
    |**字符集名称**|**Charset 说明**|**目标字符集类型，（默认值）**|  
    |big5|Big5 中文 （繁体)|NCHAR/NVARCHAR （默认值）|  
    |dec8|DEC 西部欧洲|CHAR/VARCHAR （默认值）|  
    |cp850|DOS 西部欧洲|CHAR/VARCHAR （默认值）|  
    |hp8|HP 西部欧洲|CHAR/VARCHAR （默认值）|  
    |koi8r|KOI8 R Relcom 俄语|CHAR/VARCHAR （默认值）|  
    |latin 1|cp1252 西部欧洲|CHAR/VARCHAR （默认值）|  
    |latin2|ISO 8859-2 中欧|CHAR/VARCHAR （默认值）|  
    |swe7|7 位瑞典语|CHAR/VARCHAR （默认值）|  
    |ascii|US ASCII|CHAR/VARCHAR （默认值）|  
    |ujis|EUC-JP 日语|NCHAR/NVARCHAR （默认值）|  
    |sjis|Shift JIS 日语|NCHAR/NVARCHAR （默认值）|  
    |希伯来语|ISO 8859-8 希伯来语|CHAR/VARCHAR （默认值）|  
    |tis620|TIS620 泰语|CHAR/VARCHAR （默认值）|  
    |euckr|EUC KR 朝鲜语|NCHAR/NVARCHAR （默认值）|  
    |koi8u|KOI8-U 乌克兰语|CHAR/VARCHAR （默认值）|  
    |gb2312|GB2312 中文 （简体的)|NCHAR/NVARCHAR （默认值）|  
    |希腊语|ISO 8859-7 希腊语|CHAR/VARCHAR （默认值）|  
    |cp 1250|Windows 中欧|CHAR/VARCHAR （默认值）|  
    |gbk|简体中文 GBK|NCHAR/NVARCHAR （默认值）|  
    |latin5|ISO 8859-9 土耳其语|CHAR/VARCHAR （默认值）|  
    |armscii8|ARMSCII 8 亚美尼亚语|CHAR/VARCHAR （默认值）|  
    |utf8|Utf-8 Unicode|NCHAR/NVARCHAR （默认值）|  
    |ucs2|Ucs-2 Unicode|NCHAR/NVARCHAR （默认值）|  
    |cp866|DOS 俄语|CHAR/VARCHAR （默认值）|  
    |keybcs2|DOS Kamenicky 捷克语斯洛伐克语|CHAR/VARCHAR （默认值）|  
    |macce|Mac 中欧|CHAR/VARCHAR （默认值）|  
    |macroman|Mac 西部欧洲|CHAR/VARCHAR （默认值）|  
    |cp852|DOS 中部欧洲|CHAR/VARCHAR （默认值）|  
    |latin7|ISO 8859-13 波罗|CHAR/VARCHAR （默认值）|  
    |cp 1251|Windows 西里尔文|CHAR/VARCHAR （默认值）|  
    |cp 1256|Windows 阿拉伯语|CHAR/VARCHAR （默认值）|  
    |cp 1257|Windows 波罗|CHAR/VARCHAR （默认值）|  
    |BINARY|二进制伪 charset|CHAR/VARCHAR （默认值）|  
    |geostd8|GEOSTD8 格鲁吉亚语|CHAR/VARCHAR （默认值）|  
    |cp932|对于 Windows 日文 SJIS|NCHAR/NVARCHAR （默认值）|  
    |eucjpms|对于 Windows 日文 UJIS|NCHAR/NVARCHAR （默认值）|  
  
2.  **数据库、 类别或对象节点级别上：**在数据库、 类别或对象节点级别中，字符集映射网格包含根元数据节点级别上的相同行 viz。:  
  
    1.  标题为，网格的第一列**字符设置名称**包含字符集名称。  
  
    2.  第二列的标题，**字符设置说明**包含 charset 说明。  
  
    3.  唯一的区别是网格的第三个列中的值。 第三列的标题，**目标数据类型**包含特定的字符集的映射设置。 列的值是：  
  
        -   继承 （CHAR/VARCHAR 或 NCHAR/NVARCHAR）  
  
        -   CHAR/VARCHAR  
  
        -   NCHAR/NVARCHAR  
  
> [!IMPORTANT]  
> -   在 MySQL 数据库和数据库、 类别和对象节点级别上的目标数据库之间的字符集映射中的默认值的列的根以外的其他每个级别上特定 charset**目标数据类型**应被继承。  
> -   在网格中，值**继承**使用作为后缀 '(CHAR/VARCHAR) 或 '(NCHAR/NVARCHAR) 具体取决于哪个值已从父文件夹继承通过此特定的字符集。  
  
