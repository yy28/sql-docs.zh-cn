---
title: 创建、更改和删除辅助选择性 XML 索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
ms.assetid: 45128105-833b-40a9-9cc9-1ae03ac0b52b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b96e0bb7f28349e4d0b0ed5225f9b29e58de982f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62637841"
---
# <a name="create-alter-and-drop-secondary-selective-xml-indexes"></a>创建、更改和删除辅助选择性 XML 索引
  说明如何创建新的辅助选择性 XML 索引或者更改或删除现有的辅助选择性 XML 索引。  
  
##  <a name="create"></a> 创建辅助选择性 XML 索引  
  
### <a name="how-to-create-a-secondary-selective-xml-index"></a>如何：创建辅助选择性 XML 索引  
 **使用 Transact-SQL 创建辅助选择性 XML 索引**  
 通过调用 CREATE XML INDEX 语句创建辅助选择性 XML 索引。 有关详细信息，请参阅 [创建 XML 索引&#40;选择性 XML 索引&#41;] (~ / t-sql/statements/create-xml-index-selective-xml-indexes。  
  
 **示例**  
  
 下面的示例对路径 `'pathabc'`创建辅助选择性 XML 索引。 用 CREATE SELECTIVE XML INDEX 语句创建索引时向其提供的名称标识该索引的路径。 有关详细信息，请参阅 [CREATE SELECTIVE XML INDEX (Transact-SQL)](/sql/t-sql/statements/create-selective-xml-index-transact-sql)。  
  
```sql  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="alter"></a> 更改辅助选择性 XML 索引  
 辅助选择性 XML 索引不支持 ALTER 语句。 若要更改辅助选择性 XML 索引，请删除现有索引，然后重新创建它。  
  
### <a name="how-to-alter-a-secondary-selective-xml-index"></a>如何：更改辅助选择性 XML 索引  
 **使用 Transact-SQL 更改辅助选择性 XML 索引**  
 1.  通过调用 DROP INDEX 语句删除现有辅助选择性 XML 索引。 有关详细信息，请参阅 [DROP INDEX（选择性 XML 索引）](../indexes/indexes.md)。  
  
2.  通过调用 CREATE XML INDEX 语句，用所需的选项重新创建该索引。 有关详细信息，请参阅 [创建 XML 索引&#40;选择性 XML 索引&#41;] (~ / t-sql/statements/create-xml-index-selective-xml-indexes。  
  
 **示例**  
  
 以下示例通过删除再重新创建辅助选择性 XML 索引，更改该索引。  
  
```sql  
DROP INDEX filt_sxi_index_c  
  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR  
(  
    pathabc  
)  
```  
  
  
##  <a name="drop"></a> 删除辅助选择性 XML 索引  
  
### <a name="how-to-drop-a-secondary-selective-xml-index"></a>如何：删除辅助选择性 XML 索引  
 **使用 Transact-SQL 删除辅助选择性 XML 索引**  
 通过调用 DROP INDEX 语句删除辅助选择性 XML 索引。 有关详细信息，请参阅 [DROP INDEX（选择性 XML 索引）](../indexes/indexes.md)。  
  
 **示例**  
  
 下面的示例说明 DROP INDEX 语句。  
  
```sql  
DROP INDEX ssxi_index  
ON tbl  
```  
  
  
## <a name="see-also"></a>请参阅  
 [选择性 XML 索引 (SXI)](selective-xml-indexes-sxi.md)  
  
  
