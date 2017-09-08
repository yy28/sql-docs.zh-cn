---
title: "Windows 排序规则名称 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Windows collations [SQL Server]
- names [SQL Server], collations
- collations [SQL Server], Windows collations
- Collation Designator
ms.assetid: acceef84-2c68-46e2-a021-be019b7ab14e
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7898592af503300cb1bea261d8809a81fa568155
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="windows-collation-name-transact-sql"></a>Windows 排序规则名称 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 COLLATE 子句中指定 Windows 排序规则名称。 Windows 排序规则名称是由排序规则指示符和比较样式构成的。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
<Windows_collation_name> :: =   
CollationDesignator_<ComparisonStyle>  
  
<ComparisonStyle> :: =   
{ CaseSensitivity_AccentSensitivity  [ _KanatypeSensitive ] [ _WidthSensitive ]    
}  
| { _BIN | _BIN2 }  
```  
  
## <a name="arguments"></a>参数  
 *CollationDesignator*  
 指定 Windows 排序规则使用的基本排序规则。 基本排序规则包括以下内容：  
  
-   指定按字典排序时应用的排序规则。 排序规则基于字母表或语言。  
  
-   用于存储非 Unicode 字符数据的代码页。  
  
 是一些示例：  
  
-   Latin1_General 或法语：都使用代码页 1252。  
  
-   土耳其语：使用代码页 1254。  
  
 *CaseSensitivity*  
 **CI**指定不区分大小写， **CS**指定区分大小写。  
  
 *AccentSensitivity*  
 **AI**指定不区分重音， **AS**指定重音。  
  
 *KanatypeSensitive*  
 **省略**指定假名敏感型**KS**指定区分假名的。  
  
 *WidthSensitivity*  
 **省略**指定宽度不区分**WS**指定区分全半角。  
  
 **BIN**  
 指定使用向后兼容的二进制排序顺序。  
  
 **BIN2**  
 指定使用码位比较语义的二进制排序顺序。  
  
## <a name="remarks"></a>注释  
 根据排序规则的版本，有些码位也许是未定义的。 例如比较：  
  
```  
SELECT LOWER(nchar(504) COLLATE Latin1_General_CI_AS);   
SELECT LOWER (nchar(504) COLLATE Latin1_General_100_CI_AS);  
GO  
```  
  
 当排序规则为 Latin1_General_CI_AS 时第一行返回一个大写字符，因为未在该排序规则中定义该码位。  
  
 使用某些语言时，这对避免旧排序规则至关重要。 例如，这适用于 Telegu。  
  
 在某些情况下，Windows 排序规则和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序规则可对相同查询生成不同查询计划。  
  
## <a name="examples"></a>示例  
 下面是一些 Windows 排序规则名称示例：  
  
-   **Latin1_General_100_**  
  
 排序规则使用 Latin1 General 字典排序规则，代码页 1252。 不区分大小写且区分重音。 排序规则使用 Latin1 General 字典排序规则，并映射到代码页 1252。 如果是 Windows 排序规则，则显示排序规则的版本号：_90 或 _100。 不区分大小写 (CI)，但区分重音 (AS)。  
  
-   **Estonian_CS_AS**  
  
     排序规则使用爱沙尼亚文字典排序规则，代码页 1257。 区分大小写且区分重音。  
  
-   **Latin1_General_BIN**  
  
     排序规则使用代码页 1252 和二进制排序规则。 忽略 Latin1 General 字典排序规则。  
  
## <a name="windows-collations"></a>Windows 排序规则  
 若要列出您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例支持的 Windows 排序规则，请执行以下查询。  
  
```  
SELECT * FROM sys.fn_helpcollations() WHERE name NOT LIKE 'SQL%';  
```  
  
 下表列出了 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中支持的所有 Windows 排序规则。  
  
|Windows 区域设置|排序规则版本 100|排序规则版本 90|  
|--------------------|---------------------------|--------------------------|  
|阿尔萨斯语（法国）|Latin1_General_100_|不可用|  
|阿姆哈拉语（埃塞俄比亚）|Latin1_General_100_|不可用|  
|亚美尼亚语（亚美尼亚）|Cyrillic_General_100_|不可用|  
|阿萨姆语（印度）|Assamese_100_ <sup>1</sup>|不可用|  
|巴什基尔语（俄罗斯）|Bashkir_100_|不可用|  
|巴斯克语（巴斯克）|Latin1_General_100_|不可用|  
|孟加拉语（孟加拉）|Bengali_100_<sup>1</sup>|不可用|  
|孟加拉语（印度）|Bengali_100_<sup>1</sup>|不可用|  
|波斯尼亚语（波斯尼亚和黑塞哥维那，西里尔文）|Bosnian_Cyrillic_100_|不可用|  
|波斯尼亚语（波斯尼亚和黑塞哥维那，拉丁语）|Bosnian_Latin_100_|不可用|  
|布列塔尼语（法国）|Breton_100_|不可用|  
|中文（中国澳门特别行政区）|Chinese_Traditional_Pinyin_100_|不可用|  
|中文（中国澳门特别行政区）|Chinese_Traditional_Stroke_Order_100_|不可用|  
|中文（新加坡）|Chinese_Simplified_Stroke_Order_100_|不可用|  
|科西嘉语（法国）|Corsican_100_|不可用|  
|克罗地亚语（波斯尼亚和黑塞哥维那，拉丁语）|Croatian_100_|不可用|  
|达里语（阿富汗）|Dari_100_|不可用|  
|英语（印度）|Latin1_General_100_|不可用|  
|英语（马来西亚）|Latin1_General_100_|不可用|  
|英语（新加坡）|Latin1_General_100_|不可用|  
|菲律宾语（菲律宾）|Latin1_General_100_|不可用|  
|弗里西亚语（荷兰）|Frisian_100_|不可用|  
|格鲁吉亚语（格鲁吉亚）|Cyrillic_General_100_|不可用|  
|格陵兰语（格陵兰）|Danish_Greenlandic_100_|不可用|  
|古吉拉特语（印度）|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|豪撒语（尼日利亚，拉丁语）|Latin1_General_100_|不可用|  
|印地语（印度）|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|伊博语（尼日利亚）|Latin1_General_100_|不可用|  
|因纽特语（加拿大，拉丁语）|Latin1_General_100_|不可用|  
|因纽特语（语音节）加拿大|Latin1_General_100_|不可用|  
|爱尔兰语（爱尔兰）|Latin1_General_100_|不可用|  
|日语（日本 XJIS）|Japanese_XJIS_100_|Japanese_90_、Japanese_|  
|日语（日本）|Japanese_Bushu_Kakusu_100_|不可用|  
|卡纳达语（印度）|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|高棉语（柬埔寨）|Khmer_100_<sup>1</sup>|不可用|  
|基切语（危地马拉）|Modern_Spanish_100_|不可用|  
|卢旺达语（卢旺达）|Latin1_General_100_|不可用|  
|孔卡尼语（印度）|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|老挝语（老挝人民民主共和国）|Lao_100_<sup>1</sup>|不可用|  
|下索布语（德国）|Latin1_General_100_|不可用|  
|卢森堡语（卢森堡）|Latin1_General_100_|不可用|  
|马拉雅拉姆语（印度）|Indic_General_100_<sup>1</sup>|不可用|  
|马耳他语（马耳他）|Maltese_100_|不可用|  
|毛利语（新西兰）|Maori_100_|不可用|  
|马普丹冈语（智利）|Mapudungan_100_|不可用|  
|马拉地语（印度）|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|莫霍克语（加拿大）|Mohawk_100_|不可用|  
|蒙古语（中国）|Cyrillic_General_100_|不可用|  
|尼泊尔语（尼泊尔）|Nepali_100_<sup>1</sup>|不可用|  
|挪威语（博克马尔语，挪威）|Norwegian_100_|不可用|  
|挪威语（尼诺斯克语，挪威）|Norwegian_100_|不可用|  
|奥克西唐语（法国）|French_100_|不可用|  
|奥里雅语（印度）|Indic_General_100_<sup>1</sup>|不可用|  
|普什图语（阿富汗）|Pashto_100_<sup>1</sup>|不可用|  
|波斯语（伊朗）|Persian_100_|不可用|  
|旁遮普语（印度）|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|克丘亚语（玻利维亚）|Latin1_General_100_|不可用|  
|克丘亚语（厄瓜多尔）|Latin1_General_100_|不可用|  
|克丘亚语（秘鲁）|Latin1_General_100_|不可用|  
|罗曼什语（瑞士）|Romansh_100_|不可用|  
|萨米语（伊纳里，芬兰）|Sami_Sweden_Finland_100_|不可用|  
|萨米语（律勒欧，挪威）|Sami_Norway_100_|不可用|  
|萨米语（律勒欧，瑞典）|Sami_Sweden_Finland_100_|不可用|  
|萨米语（北方，芬兰）|Sami_Sweden_Finland_100_|不可用|  
|萨米语（北方，挪威）|Sami_Norway_100_|不可用|  
|萨米语（北方，瑞典）|Sami_Sweden_Finland_100_|不可用|  
|萨米语（斯科特，芬兰）|Sami_Sweden_Finland_100_|不可用|  
|萨米语（南方，挪威）|Sami_Norway_100_|不可用|  
|萨米语（南方，瑞典）|Sami_Sweden_Finland_100_|不可用|  
|梵语（印度）|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|塞尔维亚语（波斯尼亚和黑塞哥维那，西里尔文）|Serbian_Cyrillic_100_|不可用|  
|塞尔维亚语（波斯尼亚和黑塞哥维那，拉丁语）|Serbian_Latin_100_|不可用|  
|塞尔维亚语（塞尔维亚，西里尔语）|Serbian_Cyrillic_100_|不可用|  
|塞尔维亚语（塞尔维亚，拉丁语）|Serbian_Latin_100_|不可用|  
|巴索托语/北索托语（南非）|Latin1_General_100_|不可用|  
|茨瓦纳语/博茨瓦纳（南非）|Latin1_General_100_|不可用|  
|僧伽罗语（斯里兰卡）|Indic_General_100_<sup>1</sup>|不可用|  
|斯瓦希里语（肯尼亚）|Latin1_General_100_|不可用|  
|叙利亚语（叙利亚）|Syriac_100_<sup>1</sup>|Syriac_90_|  
|塔吉克语（塔吉克斯坦）|Cyrillic_General_100_|不可用|  
|塔马塞特文（阿尔及利亚，拉丁语）|Tamazight_100_|不可用|  
|泰米尔语（印度）|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|泰卢固语（印度）|Indic_General_100_<sup>1</sup>|Indic_General_90_|  
|藏语（中国）|Tibetan_100_<sup>1</sup>|不可用|  
|土库曼语（土库曼斯坦）|Turkmen_100_|不可用|  
|维吾尔语（中国）|Uighur_100_|不可用|  
|上索布语（德国）|Upper_Sorbian_100_|不可用|  
|乌尔都语（巴基斯坦）|Urdu_100_|不可用|  
|威尔士语（英国）|Welsh_100_|不可用|  
|沃洛夫语（塞内加尔）|French_100_|不可用|  
|班图语/索萨语（南非）|Latin1_General_100_|不可用|  
|雅库特语（俄罗斯）|Yakut_100_|不可用|  
|彝语（中国）|Latin1_General_100_|不可用|  
|约鲁巴语（尼日利亚）|Latin1_General_100_|不可用|  
|祖鲁语（南非）|Latin1_General_100_|不可用|  
|不推荐使用；在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本中，在服务器级别不可用|Hindi|Hindi|  
|不推荐使用；在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本中，在服务器级别不可用|Korean_Wansung_Unicode|Korean_Wansung_Unicode|  
|不推荐使用；在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本中，在服务器级别不可用|Lithuanian_Classic|Lithuanian_Classic|  
|不推荐使用；在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 或更高版本中，在服务器级别不可用|Macedonian|Macedonian|  
  
 <sup>1</sup>仅限 Unicode 的 Windows 排序规则可以仅应用于列级别或表达式级别数据。 它们不能用作服务器或数据库排序规则。  
  
 <sup>2</sup>中文 （台湾） 排序规则，如中文 （中国澳门） 使用的简体中文规则; 与中文 （台湾），它使用代码页 950。  
  
## <a name="see-also"></a>另请参阅  
 [排序规则和 Unicode 支持](../../relational-databases/collations/collation-and-unicode-support.md)   
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [常量 &#40;Transact SQL &#41;](../../t-sql/data-types/constants-transact-sql.md)   
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [DECLARE @local_variable (Transact-SQL)](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [table &#40;Transact SQL &#41;](../../t-sql/data-types/table-transact-sql.md)   
 [sys.fn_helpcollations (Transact-SQL)](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)  
  
  
