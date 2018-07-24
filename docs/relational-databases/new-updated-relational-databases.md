---
title: 已更新 - 关系数据库文档 | Microsoft Docs
description: 显示关系数据库文档中最近更改的更新内容片段。
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: conceptual
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: relational-databases
ms.date: 04/28/2018
ms.openlocfilehash: 4f962279eb30e15b395f96417cc5e03aa1dbcfad
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39087769"
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>新文章和最近更新的文章：关系数据库文档



Microsoft 几乎每天都会更新其 [Docs.Microsoft.com](http://docs.microsoft.com/) 文档网站上的一些现有文章。 本文显示从最近更新的文章中摘录的内容。 可能还会列出新文章的链接。

本文由定期重新运行的程序生成。 摘录内容偶尔会有格式问题，还可能以源文的 markdown 格式显示。 此处不会显示任何图像。

最新的更新报告涵盖以下日期范围和主题：



- 更新日期范围：2018-02-03 到 2018-04-28&nbsp;&nbsp;&nbsp;
- 主题领域：&nbsp; 关系数据库。




&nbsp;

## <a name="new-articles-created-recently"></a>最近创建的新文章

单击以下链接可跳转到最近添加的新文章。


1. [联接 (SQL Server)](performance/joins.md)
2. [子查询 (SQL Server)](performance/subqueries.md)
3. [在 Always On 可用性组中设置复制分发数据库](replication/configure-distribution-availability-group.md)
4. [SQL 数据发现和分类](security/sql-data-discovery-and-classification.md)
5. [事务锁定和行版本控制指南](sql-server-transaction-locking-and-row-versioning-guide.md)
6. [sys.dm_os_job_object（Azure SQL 数据库）](system-dynamic-management-views/sys-dm-os-job-object-transact-sql.md)
7. [Filestream 和 FileTable 系统存储过程 (Transact-SQL)](system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>包含摘录内容的已更新文章

此部分摘录了最近大幅更新的文章中的更新内容。

此处显示的摘录与其对应的语义上下文脱离。 此外，有时摘录会与实际文章中此摘录周围的重要 markdown 语法元素脱离。 因此，这些摘录仅可用于一般指导。 摘录只是帮助你确定自己是否有兴趣花时间点击并访问实际文章。

鉴于以上原因及其他原因，请不要复制这些摘录中的代码，也不要将摘录当作确切事实。 请转而访问实际文章。





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>最近更新的文章的紧凑列表

此紧凑列表中的链接指向“摘录”部分中列出的所有更新后文章。

1. [使用格式化文件跳过表列 (SQL Server)](#TitleNum_1)
2. [SQL Server 中的 JSON 数据](#TitleNum_2)
3. [查询处理体系结构指南](#TitleNum_3)
4. [教程：为复制准备 SQL Server - 发布服务器、分发服务器、订阅服务器](#TitleNum_4)
5. [教程：在两个完全连接的服务器之间配置复制（事务）](#TitleNum_5)
6. [教程：配置服务器和移动客户端之间的复制（合并）](#TitleNum_6)
7. [使用全文搜索查询](#TitleNum_7)
8. [使用 Azure SQL 数据库和数据仓库的自带密钥支持进行透明数据加密](#TitleNum_8)
9. [PowerShell 和 CLI：使用 Azure Key Vault 中的自有密钥启用透明数据加密](#TitleNum_9)
10. [关于变更数据捕获 (SQL Server)](#TitleNum_10)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-use-a-format-file-to-skip-a-table-column-sql-serverimport-exportuse-a-format-file-to-skip-a-table-column-sql-servermd"></a>1.&nbsp; [使用格式化文件跳过表列 (SQL Server)](import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)

更新日期：2018-04-13 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([下一篇](#TitleNum_2))

<!-- Source markdown line 221.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 167916d79c5de1e7f13990cb7acc41ceb541b9a7 cb92eb201292294e3397879c98f353fba45f1c1c  (PR=0  ,  Filename=use-a-format-file-to-skip-a-table-column-sql-server.md  ,  Dirpath=docs\relational-databases\import-export\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**使用 OPENROWSET(BULK...)**


若要使用 XML 格式化文件通过 `OPENROWSET(BULK...)` 跳过表列，必须提供选择列表以及目标表中列的显式列表，如下所示：

```
    INSERT ...<column_list> SELECT <column_list> FROM OPENROWSET(BULK...)
```

下面的示例使用 `OPENROWSET` 大容量行集提供程序和 `myTestSkipCol2.xml` 格式化文件。 此示例将 `myTestSkipCol2.dat` 数据文件大容量导入至 `myTestSkipCol` 表。 语句中包含了需要提供的选择列表以及目标表中列的显式列表。

在 SSMS 中，运行以下代码。 更新计算机上示例文件位置的文件系统路径。

```
USE WideWorldImporters;
GO
INSERT INTO myTestSkipCol
  (Col1,Col3)
    SELECT Col1,Col3
      FROM  OPENROWSET(BULK  'C:\myTestSkipCol2.Dat',
      FORMATFILE='C:\myTestSkipCol2.Xml'
       ) as t1 ;
GO
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-json-data-in-sql-serverjsonjson-data-sql-servermd"></a>2.&nbsp; [SQL Server 中的 JSON 数据](json/json-data-sql-server.md)

更新日期：2018-04-13 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一篇](#TitleNum_1) | [下一篇](#TitleNum_3))

<!-- Source markdown line 145.  ms.author= "jovanpop".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 19e276637a463b412f2c29a84f9fb7d0b0f5fcc5 e2f2e8b4732779b3f24561cc0c4da3a958f4edbb  (PR=0  ,  Filename=json-data-sql-server.md  ,  Dirpath=docs\relational-databases\json\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



JSON 文档可能包含无法直接映射到标准关系列中的子元素和层次结构数据。 在这种情况下，可通过将父实体与子数组联接，平展 JSON 层次结构。

在下面的示例中，数组中的第二个对象包含表示人员技能的子数组。 每个子对象都可使用附加 `OPENJSON` 函数调用进行分析：

```
DECLARE @json NVARCHAR(MAX)
SET @json =
N'[
       { "id" : 2,"info": { "name": "John", "surname": "Smith" }, "age": 25 },
       { "id" : 5,"info": { "name": "Jane", "surname": "Smith", "skills": ["SQL", "C#", "Azure"] }, "dob": "2005-11-04T12:00:00" }
 ]'

SELECT *
FROM OPENJSON(@json)
  WITH (id int 'strict $.id',
        firstName nvarchar(50) '$.info.name', lastName nvarchar(50) '$.info.surname',
        age int, dateOfBirth datetime2 '$.dob',
    skills nvarchar(max) '$.skills' as json)
    outer apply openjson( a.skills )
                     with ( skill nvarchar(8) '$' ) as b
```
首个 `OPENJSON` 中返回技能数组，作为原始 JSON 文本片段，并使用 `APPLY` 运算符传递给其他 `OPENJSON` 函数。 第二个 `OPENJSON` 函数将分析 JSON 数组并将字符串值返回为单列行集，这一行集将与第一个 `OPENJSON` 的结果联接。
此查询的结果如下表所示：

**结果**

|id|firstName|lastName|age|dateOfBirth|技能|
|--------|---------------|--------------|---------|-----------------|----------|
|2|John|Smith|25|||
|5|Jane|Smith||2005-11-04T12:00:00|SQL|
|5|Jane|Smith||2005-11-04T12:00:00|C#|
|5|Jane|Smith||2005-11-04T12:00:00|Azure|

`OUTER APPLY OPENJSON` 将联接一级实体和子数组，并返回平展后的结果集。 由于 JOIN，将对每个技能重复第二行。




&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-query-processing-architecture-guidequery-processing-architecture-guidemd"></a>3.&nbsp; [查询处理体系结构指南](query-processing-architecture-guide.md)

更新日期：2018-04-13 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一篇](#TitleNum_2) | [下一篇](#TitleNum_4))

<!-- Source markdown line 34.  ms.author= "jroth".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 96d91b39acdb2f32aaff323e374e92d6f229d241 2c1d2f8585632ada174388399782dc3ed2721dba  (PR=0  ,  Filename=query-processing-architecture-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**逻辑运算符的优先顺序**


当一个语句中使用了多个逻辑运算符时，计算顺序依次为：`NOT`、`AND`最后是 `OR`。 算术运算符和位运算符优先于逻辑运算符处理。 有关详细信息，请参阅[运算符优先级]。

在下面的示例中，颜色条件适用于产品型号 21，而不适用于产品型号 20，因为 `AND` 的优先级高于 `OR`。

```
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE ProductModelID = 20 OR ProductModelID = 21
  AND Color = 'Red';
GO
```

可以通过添加括号强制先计算 `OR` 来改变查询的含义。 以下查询只查找型号 20 和 21 中红色的产品。

```
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE (ProductModelID = 20 OR ProductModelID = 21)
  AND Color = 'Red';
GO
```

因为运算符存在优先级，所以使用括号（即使不需要）可以提高查询的可读性，并减少出现细微错误的可能性。 使用括号不会造成重大的性能损失。 下面的示例比原始示例更可读，虽然它们在语义上是相同的。

```
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE ProductModelID = 20 OR (ProductModelID = 21
  AND Color = 'Red');
GO
```




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-tutorial-prepare-sql-server-for-replication---publisher-distributor-subscriberreplicationtutorial-preparing-the-server-for-replicationmd"></a>4.&nbsp; [教程：为复制准备 SQL Server - 发布服务器、分发服务器、订阅服务器](replication/tutorial-preparing-the-server-for-replication.md)

更新日期：2018-04-13 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一篇](#TitleNum_3) | [下一篇](#TitleNum_5))

<!-- Source markdown line 56.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6e5caedacff193ce79bdd98708ae1b9dc91f0a8f 9f7af4d3f8b1cffd048db2a5b29fc9e6013f5ed2  (PR=0  ,  Filename=tutorial-preparing-the-server-for-replication.md  ,  Dirpath=docs\relational-databases\replication\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



- 安装 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安装 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
- 下载 [AdventureWorks 示例数据库](https://github.com/Microsoft/sql-server-samples/releases)。 有关在 SSMS 中还原数据库的说明，请参阅[还原数据库](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。

>[!NOTE]
> - 在相差两个版本以上的 SQL Server 上不支持复制。 有关详细信息，请参阅[复制拓扑中受支持的 SQL 版本](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/)。
> - 在 {Included-Content-Goes-Here} 中，必须使用属于 sysadmin 固定服务器角色成员的登录名连接到发布服务器和订阅服务器。 有关 sysadmin 角色的详细信息，请参阅[服务器级别角色](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/server-level-roles)。


本教程的预计学时：30 分钟

**为复制创建 Windows 帐户**

在本部分中，将创建 Windows 帐户以运行复制代理。 您将在本地服务器上为以下代理创建一个单独的 Windows 帐户：

|代理|位置|帐户名|
|---------|------------|----------------|
|快照代理|发布服务器|<*machine_name*>\repl_snapshot|



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-tutorial-configure-replication-between-two-fully-connected-servers-transactionalreplicationtutorial-replicating-data-between-continuously-connected-serversmd"></a>5.&nbsp; [教程：在两个完全连接的服务器之间配置复制（事务）](replication/tutorial-replicating-data-between-continuously-connected-servers.md)

更新日期：2018-04-13 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一篇](#TitleNum_4) | [下一篇](#TitleNum_6))

<!-- Source markdown line 162.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0d74f984d0ffc01cce0376837e6d94df3c5654d7 4ecf4d724286130927dd43687d6845059af6f9b7  (PR=0  ,  Filename=tutorial-replicating-data-between-continuously-connected-servers.md  ,  Dirpath=docs\relational-databases\replication\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**创建事务发布的订阅**

在此节中，介绍如何将订阅服务器添加到先前创建的发布中。 本教程使用远程订阅服务器 (NODE2\SQL2016)，但订阅也可在本地添加到发布服务器。

**创建订阅**


1.  在 {Included-Content-Goes-Here} 中连接到发布服务器，然后依次展开服务器节点和“复制”文件夹。

2.  在“本地发布”文件夹中，右键单击“AdvWorksProductTrans”发布，然后选择“新建订阅”。  新建订阅向导将启动。

    “新建订阅”

3.  在“发布”页上，选择“AdvWorksProductTrans”，然后选择“下一步”：

    选择 Tran 发布服务器

4.  在“分发代理位置”页上，选择“在分发服务器上运行所有代理”，然后选择“下一步”。  有关请求订阅和推送订阅的详细信息，请参阅[订阅发布](https://docs.microsoft.com/sql/relational-databases/replication/subscribe-to-publications)：

    在 Dist 运行代理

5.  在“订阅服务器”页上，如果未显示订阅服务器实例的名称，选择“添加订阅服务器”，然后从下拉列表选择“添加 SQL Server 订阅服务器”。 这将启动“连接到服务器”对话框。 输入订阅服务器实例名称，然后选择“连接”。



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-tutorial-configure-replication-between-a-server-and-mobile-clients-mergereplicationtutorial-replicating-data-with-mobile-clientsmd"></a>6.&nbsp; [教程：配置服务器和移动客户端之间的复制（合并）](replication/tutorial-replicating-data-with-mobile-clients.md)

更新日期：2018-04-13 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一篇](#TitleNum_5) | [下一篇](#TitleNum_7))

<!-- Source markdown line 93.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0eed78dfe83c88358c030539a2b25d11ef5ec2d3 79b2a3f32c940fede94b11ad2a3ef8a00b911a39  (PR=0  ,  Filename=tutorial-replicating-data-with-mobile-clients.md  ,  Dirpath=docs\relational-databases\replication\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



“Employee”表包含数据类型为 hierarchyid 的列 (OrganizationNode)，仅 SQL 2017 中的复制支持。 如果使用低于 SQL 2017 的内部版本，会在屏幕底部看到一条消息，通知你在双向复制中使用此列可能出现数据丢失。 对于此教程，可以忽略此错误消息。 但是，除非使用受支持的内部版本，否则不应在生产坏境中复制此数据类型。 有关如何复制 hierarchyid 数据类型的详细信息，请参阅[在复制中使用 Hierarchyid 列](https://docs.microsoft.com/sql/t-sql/data-types/hierarchyid-data-type-method-reference#using-hierarchyid-columns-in-replicated-tables)


-  在“筛选表行”页上，选择“添加”，然后选择“添加筛选器”。

-  在“添加筛选器”对话框中，在“选择要筛选的表”中选择“Employee (HumanResources)”。 选择 LoginID 列，再选择向右键以将此列添加到筛选查询的 WHERE 子句，并将 WHERE 子句修改如下：

    ```
    WHERE [LoginID] = HOST_NAME()
    ```

    A. 选择“此表中的行将仅转到一个订阅”，再选择“确定”：

    添加筛选器



- 在“筛选表行”页上，选择“Employee (Human Resources)”，选择“添加”，然后选择“添加联接以扩展所选筛选器”。

    A. 在“添加联接”对话框的“联接的表”下，选择“Sales.SalesOrderHeader”。 在“手动编写联接语句”框中，按如下所示完成联接语句：



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-query-with-full-text-searchsearchquery-with-full-text-searchmd"></a>7.&nbsp; [使用全文搜索查询](search/query-with-full-text-search.md)

更新日期：2018-04-13 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一篇](#TitleNum_6) | [下一篇](#TitleNum_8))

<!-- Source markdown line 247.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5ec67b56aa0a6eadadbcfa8b73b6726e75eca2bb 4eb108b202d3dd035a312bac7872cf02bcf31cfa  (PR=0  ,  Filename=query-with-full-text-search.md  ,  Dirpath=docs\relational-databases\search\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**有关派生词搜索的详细信息**


*变形*是动词的不同时态和语态形式，或是名词的单数和复数形式。

例如，搜索词“drive”的变形。 如果表中不同的行包含词“drive”、“drives”、“drove”、“driving”和“driven”，则这些词都会出现在结果集中，原因是它们每一个都可以从词 drive 变形而来。

[FREETEXT] 和 [FREETEXTTABLE] 默认情况下查找所有指定词的变形。 [CONTAINS] 和 [CONTAINSTABLE] 支持可选的 `INFLECTIONAL` 参数。

**搜索特定词的同义词**


*同义词库*为词定义用户指定的同义词。 有关同义词库文件的详细信息，请参阅[为全文搜索配置和管理同义词库文件]。

例如，如果将项“{car, automobile, truck, van}”添加到同义词库，则可以搜索单词“car”的同义词库形式。 所查询表中所有包括单词“automobile”、“truck”、“van”或“car”的行都会出现在结果集中，因为所有这些单词都属于包含单词“car”的同义词扩展集。

[FREETEXT] 和 [FREETEXTTABLE] 默认情况下使用同义词库。 [CONTAINS] 和 [CONTAINSTABLE] 支持可选的 `THESAURUS` 参数。



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-transparent-data-encryption-with-bring-your-own-key-support-for-azure-sql-database-and-data-warehousesecurityencryptiontransparent-data-encryption-byok-azure-sqlmd"></a>8.&nbsp; [使用 Azure SQL 数据库和数据仓库的自带密钥支持进行透明数据加密](security/encryption/transparent-data-encryption-byok-azure-sql.md)

更新日期：2018-04-24 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一篇](#TitleNum_7) | [下一篇](#TitleNum_9))

<!-- Source markdown line 110.  ms.author= "aliceku".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9527658848d430bf0148be84474a75b232cbd112 70ed2a129c580962384f808e8526673957f00d2c  (PR=5662  ,  Filename=transparent-data-encryption-byok-azure-sql.md  ,  Dirpath=docs\relational-databases\security\encryption\  ,  MergeCommitSha40=91a9c812739a1c9a6ec9e7b8cda71ee1f5adae3d) -->



**如何使用 Azure Key Vault 配置 Geo-DR**


要保持用于加密数据库的 TDE 保护程序的高可用性，需要基于现有的或所需的 SQL 数据库故障转移组或活动异地复制实例配置冗余 Azure Key Vault。  每个异地复制服务器都需要一个单独的 Key Vault，该 Key Vault 必须与服务器位于同一个 Azure 区域。 如果因为一个区域发生中断而无法访问主数据库，且触发了故障转移，则可以使用辅助密钥保管库让辅助数据库进行接管。

对于异地复制的 Azure SQL 数据库，需要以下 Azure Key Vault 配置：
- 区域中需要有一个具有 Key Vault 的主数据库和一个具有 Key Vault 的辅助数据库。
- 至少需要一个辅助数据库，最多支持四个辅助数据库。
- 不支持链式辅助数据库。

以下部分将详细说明安装和配置步骤。

**Azure Key Vault 配置步骤**


- 安装 [PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-5.6.0)
- 使用 Key Vault 中的 [PowerShell 启用“软删除”属性](https://docs.microsoft.com/azure/key-vault/key-vault-soft-delete-powershell)，在两个不同区域创建两个 Azure Key Vault（该选项在 AKV 门户中还不可用，但 SQL 需要该选项）。
- 这两个 Azure Key Vault 都必须位于在相同 Azure 地域中可用的两个区域，才能备份和恢复密钥。  如果需要将两个 Key Vault 位于不同地区以满足 SQL Geo-DR 要求，请遵循 [BYOK 过程](https://docs.microsoft.com/azure/key-vault/key-vault-hsm-protected-keys)，该过程允许从本地 HSM 导入密钥。



&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-powershell-and-cli-enable-transparent-data-encryption-using-your-own-key-from-azure-key-vaultsecurityencryptiontransparent-data-encryption-byok-azure-sql-configuremd"></a>9.&nbsp; [PowerShell 和 CLI：使用 Azure Key Vault 中的自有密钥启用透明数据加密](security/encryption/transparent-data-encryption-byok-azure-sql-configure.md)

更新日期：2018-04-24 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一篇](#TitleNum_8) | [下一篇](#TitleNum_10))

<!-- Source markdown line 196.  ms.author= "aliceku".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a0e00f5701d9a493f503a477c69097ce65aba174 721e8fb856a55ee1e8e9e7fc06036a03adab647b  (PR=5662  ,  Filename=transparent-data-encryption-byok-azure-sql-configure.md  ,  Dirpath=docs\relational-databases\security\encryption\  ,  MergeCommitSha40=91a9c812739a1c9a6ec9e7b8cda71ee1f5adae3d) -->



**CLI 的先决条件**


- 必须有 Azure 订阅，并且成为订阅中的管理员。
- [推荐但可选]具有硬件安全性模块 (HSM) 或本地密钥存储，用于创建 TDE 保护程序密钥材料的本地副本。
- 命令行接口版本 2.0 或更高版本。 若要安装最新版本并连接到 Azure 订阅，请参阅[安装和配置 Azure 跨平台命令行接口 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)。
- 创建用于 TDE 的 Azure Key Vault 和密钥。
   - [使用 CLI 2.0 管理 Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-manage-with-cli2)
   - [有关使用硬件安全模块 (HSM) 和 Key Vault 的说明](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
 - 密钥保管库必须具有以下用于 TDE 的属性：
   - [软删除](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete)
   - [如何将 Key Vault 软删除与 CLI 配合使用](https://docs.microsoft.com/azure/key-vault/key-vault-soft-delete-cli)
- 密钥必须具有以下用于 TDE 的属性：
   - 无过期日期
   - 未禁用
   - 能够执行 get、wrap key 和 unwrap key 操作

**步骤：创建服务器并将 Azure AD 标识分配给服务器**

      cli
      # create server (with identity) and database



&nbsp;

&nbsp;

---

<a name="TitleNum_10"/>

### <a name="10-nbsp-about-change-data-capture-sql-servertrack-changesabout-change-data-capture-sql-servermd"></a>10.&nbsp; [关于变更数据捕获 (SQL Server)](track-changes/about-change-data-capture-sql-server.md)

更新日期：2018-04-17 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([上一篇](#TitleNum_9))

<!-- Source markdown line 112.  ms.author= "jroth".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 588bff652adefd719e799e9777a416b70184c5f8 77ebdbb1b98b24054d5c5afbb3f1d40e94d1e6bc  (PR=5574  ,  Filename=about-change-data-capture-sql-server.md  ,  Dirpath=docs\relational-databases\track-changes\  ,  MergeCommitSha40=bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68) -->



**使用数据库和表排序规则的差异**


请务必了解在数据库与为变更数据捕获而配置的表的列之间具有不同的排序规则。 CDC 使用临时存储来填充副表。 如果表的 CHAR 或 VARCHAR 列的排序规则与数据库排序规则不同，并且这些列存储了非 ASCII 字符（例如双字节 DBCS 字符），则 CDC 可能无法将更改后的数据与基表中的数据保持一致。 这是因为临时存储变量不能包含与之关联的排序规则。

请考虑以下方法之一，确保变更数据捕获与基表保持一致：

- 将 NCHAR 或 NVARCHAR 数据类型用于包含非 ASCII 数据的列。

- 或者，将相同的排序规则用于列和数据库。

例如，如果有使用 SQL_Latin1_General_CP1_CI_AS 排序规则的数据库，请考虑下表：

```
CREATE TABLE T1(
     C1 INT PRIMARY KEY,
     C2 VARCHAR(10) collate Chinese_PRC_CI_AI)
```

CDC 可能无法为列 C2 捕获二进制数据，因为它的排序规则不同 (Chinese_PRC_CI_AI)。 使用 NVARCHAR 可避免此问题：

```
CREATE TABLE T1(
     C1 INT PRIMARY KEY,
     C2 NVARCHAR(10) collate Chinese_PRC_CI_AI --Unicode data type, CDC works well with this data type)
```







## <a name="similar-articles-about-new-or-updated-articles"></a>新文章或更新的文章的类似文章

本节列出了 GitHub.com 公共存储库 ([MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/)) 内其他主题区域中与最近更新的文章非常相似的文章。



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>主题区域具有新的或最近更新的文章

- [新文章和更新的文章 (11+6)：SQL 高级分析文档](../advanced-analytics/new-updated-advanced-analytics.md)&nbsp; &nbsp;
- [新文章和更新的文章 (18+0)：Analysis Services for SQL 文档](../analysis-services/new-updated-analysis-services.md)&nbsp; &nbsp;
- [新文章和更新的文章 (218+14)：连接到 SQL 文档](../connect/new-updated-connect.md)
- [新文章和更新的文章 (14+0)：SQL 数据库引擎文档](../database-engine/new-updated-database-engine.md)&nbsp; &nbsp;
- [新文章和更新的文章 (3+2)： SQL Integration Services 文档](../integration-services/new-updated-integration-services.md)&nbsp; &nbsp;
- [新文章和更新的文章 (3+3)： Linux for SQL 文档](../linux/new-updated-linux.md)&nbsp; &nbsp;
- [新文章和更新的文章 (7+10)：SQL 关系数据库文档](../relational-databases/new-updated-relational-databases.md)&nbsp; &nbsp;
- [新文章和更新的文章 (0+2)：Reporting Services for SQL 文档](../reporting-services/new-updated-reporting-services.md)&nbsp; &nbsp;
- [新文章和更新的文章 (1+3)：SQL Operations Studio 文档](../sql-operations-studio/new-updated-sql-operations-studio.md)&nbsp; &nbsp;
- [新文章和更新的文章 (2+3)：Microsoft SQL Server 文档](../sql-server/new-updated-sql-server.md)&nbsp; &nbsp;
- [新文章和更新的文章 (1+1)：SQL Server Data Tools (SSDT) 文档](../ssdt/new-updated-ssdt.md)&nbsp; &nbsp;
- [新文章和更新的文章 (5+2)：SQL Server Management Studio (SSMS) 文档](../ssms/new-updated-ssms.md)&nbsp; &nbsp;
- [新文章和更新的文章 (0+2)：Transact-SQL 文档](../t-sql/new-updated-t-sql.md)&nbsp; &nbsp;
- [新文章和更新的文章 (1+1)：SQL 工具文档](../tools/new-updated-tools.md)&nbsp; &nbsp;



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>主题区域没有新的或最近更新的文章

- [新文章和更新的文章 (0+0)：SQL 分析平台系统文档](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [新的和更新的文章 (0+0)：Data Quality Services for SQL 文档](../data-quality-services/new-updated-data-quality-services.md)
- [新的和更新的文章 (0+0)：SQL 数据挖掘扩展插件 (DMX) 文档](../dmx/new-updated-dmx.md)
- [新文章和更新的文章 (0+0)：Master Data Services (MDS) for SQL 文档](../master-data-services/new-updated-master-data-services.md)
- [新的和更新的文章 (0+0)：SQL 多维表达式 (MDX) 文档](../mdx/new-updated-mdx.md)
- [新的和更新的文章 (0+0)：SQL 开放式数据库连接 (ODBC) 文档](../odbc/new-updated-odbc.md)
- [新的和更新的文章 (0+0)：PowerShell for SQL 文档](../powershell/new-updated-powershell.md)
- [新的和更新的文章 (0+0)：SQL 示例文档](../samples/new-updated-samples.md)
- [新的和更新的文章 (0+0)：SQL Server Migration Assistant (SSMA) 文档](../ssma/new-updated-ssma.md)
- [新的和更新的文章 (0+0)：XQuery for SQL 文档](../xquery/new-updated-xquery.md)

