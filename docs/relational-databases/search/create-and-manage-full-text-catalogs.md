---
title: "创建和管理全文索引目录 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "全文目录 [SQL Server], 创建"
  - "全文搜索 [SQL Server], 使用 SQL Server Management Studio"
ms.assetid: 824b7131-44a6-4815-89e6-62b7bab060e3
caps.latest.revision: 21
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 20
---
# 创建和管理全文索引目录
  全文目录是虚拟对象，并不属于任何文件组；它是表示一组全文索引的逻辑概念。  
  
##  <a name="creating"></a> 创建全文目录  
  
#### 创建全文目录  
  
1.  在对象资源管理器中，展开服务器，展开“数据库”，然后展开要在其中创建全文目录的数据库。  
  
2.  展开“存储”，然后右键单击“全文目录”。  
  
3.  选择“新建全文目录”。  
  
4.  在“新建全文目录”对话框中，指定要重新创建的目录的信息。 有关详细信息，请参阅[新建全文目录（常规页）](../Topic/New%20Full-Text%20Catalog%20\(General%20Page\).md)。  
  
    > [!NOTE]  
    >  全文目录 ID 从 00005 开始，每创建一个新目录，其 ID 值就会递增 1。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
   
  
##  <a name="props"></a> 查看全文目录的属性  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函数（例如 FULLTEXTCATALOGPROPERTY）可用来获取与全文索引相关的各种属性的值。 此信息可用于全文搜索的管理和故障排除。  
  
 下表列出了与全文目录相关的属性。  
  
|属性|说明|函数|  
|--------------|-----------------|--------------|  
|**AccentSensitivity**|区分重音设置。|[FULLTEXTCATALOGPROPERTY](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)|  
|**ImportStatus**|是否将导入全文目录。|FULLTEXTCATALOGPROPERTY|  
|**IndexSize**|全文目录的大小，以 MB 为单位。|FULLTEXTCATALOGPROPERTY|  
|**ItemCount**|全文目录中当前包含的全文索引项的数目。|FULLTEXTCATALOGPROPERTY|  
|**MergeStatus**|是否正在进行主合并。|FULLTEXTCATALOGPROPERTY|  
|**PopulateCompletionAge**|上一次全文索引填充的完成时间与 01/01/1990 00:00:00 之间的时间差（秒）。|FULLTEXTCATALOGPROPERTY|  
|**PopulateStatus**|填充状态。<br /><br /> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|FULLTEXTCATALOGPROPERTY|  
|**UniqueKeyCount**|全文目录中的唯一键数。|FULLTEXTCATALOGPROPERTY|  
  
   
  
##  <a name="rebuildone"></a> 重新生成全文目录  
  
#### 重新生成全文目录  
  
1.  在对象资源管理器中，展开服务器，展开“数据库”，然后展开包含要重新生成的全文目录的数据库。  
  
2.  展开 **“存储”**，然后展开 **“全文目录”**。  
  
3.  右键单击要重新生成的全文目录的名称，并选择“重新生成”。  
  
4.  对于问题**是否要删除并重新生成全文目录?**，请单击“确定”。  
  
5.  在“重新生成全文目录”对话框中，单击“关闭”。  
  
   
  
##  <a name="rebuildall"></a> 为数据库重新生成所有全文目录  
  
#### 为数据库重新生成全文目录  
  
1.  在对象资源管理器中，展开服务器，展开“数据库”，然后展开包含要重新生成的全文目录的数据库。  
  
2.  展开“存储”，然后右键单击“全文目录”。  
  
3.  选择 **“全部重新生成”**。  
  
4.  对于问题**是否要删除并重新生成所有全文目录?**，请单击“确定”。  
  
5.  在“重新生成所有全文目录”对话框中，单击“关闭”。  
  
  
  
##  <a name="removing"></a> 从数据库中删除全文目录  
  
#### 从数据库中删除全文目录  
  
1.  在对象资源管理器中，展开服务器，展开“数据库”，然后展开要删除的全文目录所在的数据库。  
  
2.  展开 **“存储”**，然后展开 **“全文目录”**。  
  
3.  右键单击要删除的全文目录，然后选择“删除”。  
  
4.  在 **“删除对象”** 对话框中，单击 **“确定”**。  
  
  
## 另请参阅  
 [CREATE FULLTEXT CATALOG (Transact-SQL)](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)  
  
  