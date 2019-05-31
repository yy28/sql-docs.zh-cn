---
title: 具有安全 Enclave 的 Always Encrypted（数据库引擎）| Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 377c2d95564e7348bdfb5de9480c7c7f5004c7f7
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2019
ms.locfileid: "65938158"
---
# <a name="always-encrypted-with-secure-enclaves"></a>具有安全 Enclave 的 Always Encrypted
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]


具有安全 Enclave 的 Always Encrypted 为 [Always Encrypted](always-encrypted-database-engine.md) 功能提供其他功能。

SQL Server 2016 中引入的 Always Encrypted 可保护敏感数据的机密性免受 SQL Server 的恶意软件以及具有高度特权但未经授权  的用户的攻击。 具有高度特权但未经授权的用户包括 DBA、计算机管理员、云管理员，或可以合法访问服务器实例、硬件等但不应有权访问部分或全部实际数据的任何其他用户。 

到目前为止，Always Encrypted 通过在客户端加密数据并且从不允许数据或相应的加密密钥以纯文本形式显示在 SQL Server 引擎中来保护数据。 因此，数据库内的加密列上的功能受到严格限制。 SQL Server 可以对加密数据执行的唯一操作是相等比较（相等比较仅适用于确定性加密）。 数据库内不支持所有其他操作，包括加密操作（初始数据加密或密钥轮替）或富计算（例如，模式匹配）。 用户需要将数据移出数据库才能对客户端执行这些操作。

 具有安全 enclave 的 Always Encrypted 通过允许在服务器端对安全 enclave 内的纯文本数据进行计算来解决这些限制。 安全 enclave 是 SQL Server 进程内受保护的内存区域，并充当用于处理 SQL Server 引擎中的敏感数据的受信任执行环境。 安全 enclave 显示为托管计算机上的其余 SQL Server 和其他进程的黑盒。 无法从外部查看 enclave 内的任何数据或代码，即使采用调试程序也是如此。  


Always Encrypted 使用安全 enclave，如下图中所示：

![数据流](./media/always-encrypted-enclaves/ae-data-flow.png)



解析应用程序的查询时，SQL Server 引擎会确定查询是否包含对需要使用安全 enclave 的加密数据执行的任何操作。 对于需要访问安全 enclave 的查询：

- 客户端驱动程序向安全 enclave 发送操作所需的列加密密钥（通过安全通道）。 
- 然后，客户端驱动程序提交要执行的查询以及加密的查询参数。

在查询处理期间，不会在 SQL Server 引擎中以纯文本形式公开安全 enclave 之外的数据或列加密密钥。 SQL Server 引擎向安全 enclave 委派针对加密列的加密操作和计算。 如果需要，安全 enclave 会解密查询参数和/或加密列中存储的数据，并执行所请求的操作。

## <a name="why-use-always-encrypted-with-secure-enclaves"></a>为何使用具有安全 enclave 的 Always Encrypted？

借助安全 enclave，Always Encrypted 可保护敏感数据的机密性，同时提供以下优势：

- **就地加密** – 针对敏感数据的加密操作（例如：初始数据加密或轮替列加密密钥）在安全 enclave 内执行，且不需要将数据移出数据库。 可以使用 ALTER TABLE Transact-SQL 语句执行就地加密，且不需要使用 SSMS 中的 Always Encrypted 向导或 Set-SqlColumnEncryption PowerShell cmdlet。

- **富计算（预览）** – 在安全 enclave 内支持针对加密列的操作，包括模式匹配（LIKE 谓词）和范围比较，这样会将 Always Encrypted 解锁到需要在数据库系统内执行此类计算的广泛应用和方案。

> [!IMPORTANT]
> 在 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 中，富计算正在等待多项性能优化，包括有限的功能（无索引等），并且当前默认处于禁用状态。 若要启用富计算，请参阅[启用富计算](configure-always-encrypted-enclaves.md#configure-a-secure-enclave)。

在 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)][ 中，具有安全 enclave 的 Always Encrypted 使用](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/)基于虚拟化的安全 (VBS) 保护 Windows 中的内存 enclave（也称为虚拟安全模式或 VSM enclave）。

## <a name="secure-enclave-attestation"></a>安全 Enclave 证明

SQL Server 引擎内的安全 enclave 可以访问加密数据库列中存储的敏感数据以及相应的纯文本列加密密钥。 在向 SQL Server 提交涉及到 enclave 计算的查询之前，应用程序内的客户端驱动程序必须基于给定的技术（例如，VBS）验证安全 enclave 是否是正版 enclave，以及是否已签署 enclave 以在 enclave 内运行。 

验证 enclave 的过程称为“enclave 证明”  ，通常包括应用程序内用于连接外部证明服务的客户端驱动程序（有时还包括 SQL Server）。 证明过程的细节取决于 enclave 技术和证明服务。

SQL Server 支持 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 中的 VBS 安全 enclave 的证明过程是 Windows Defender System Guard 运行时证明，该证明将主机保护者服务 (HGS) 用作证明服务。 需要在你的环境中配置 HGS 并注册用于托管 HGS 中的 SQL Server 实例的计算机。 还必须使用 HGS 证明配置客户端应用程序或工具（例如，SQL Server Management Studio）。

## <a name="secure-enclave-providers"></a>安全 Enclave 提供程序

若要使用具有安全 enclave 的 Always Encrypted，应用程序必须使用支持该功能的客户端驱动程序。 在 [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] 中，应用程序必须使用 .NET Framework 4.7.2 和用于 SQL Server 的 .NET Framework 数据提供程序。 此外，.NET 应用程序还必须使用特定于 enclave 类型（例如，VBS）的安全 enclave 提供程序  和所使用的证明服务（例如，HGS）进行配置。 支持的 enclave 提供程序在 NuGet 包中单独装运，你需要将该包与你的应用程序集成。 Enclave 提供程序实施证明协议的客户端逻辑，用于使用给定类型的安全 enclave 建立安全通道。

## <a name="enclave-enabled-keys"></a>已启用 enclave 的密钥

具有安全 enclave 的 Always Encrypted 引入了已启用 enclave 的密钥的概念：

- **已启用 enclave 的列主密钥** – 具有数据库内的列主密钥元数据对象中指定的 ENCLAVE_COMPUTATIONS 属性的列主密钥。 列主密钥元数据对象还必须包含元数据属性的有效签名。
- **已启用 enclave 的列加密密钥** – 使用已启用 enclave 的列主密钥加密的列加密密钥。

当 SQL Server 引擎确定需要在安全 enclave 内执行查询中指定的操作时，SQL Server 引擎会请求客户端驱动程序共享使用安全 enclave 进行计算所需的列加密密钥。 仅当密钥已启用 enclave（即，使用已启用 enclave 的列主密钥进行加密）且已进行正确签名时，客户端驱动程序才会共享列加密密钥。 否则，查询将失败。

## <a name="enclave-enabled-columns"></a>已启用 enclave 的列

已启用 enclave 的列是使用已启用 enclave 的列加密密钥加密的数据库列。 可用于已启用 enclave 的列的功能取决于列所使用的加密类型。

- 确定性加密  - 使用确定性加密的已启用 enclave 的列支持就地加密，但不支持安全 enclave 内的任何其他操作。 支持相等比较，但通过比较已加密文本（在 enclave 之外）在 enclave 之外执行。  
- 随机加密  - 使用随机加密的已启用 enclave 的列支持就地加密以及安全 enclave 内的富计算。 支持的富计算是模式匹配和[比较运算符](https://docs.microsoft.com/sql/t-sql/language-elements/comparison-operators-transact-sql)，包括相等比较。

有关加密类型的详细信息，请参阅 [Always Encrypted 加密](always-encrypted-cryptography.md)。

下表总结了可用于加密列的功能，具体取决于列是否使用已启用 enclave 的列加密密钥以及加密类型。

| **运算**| **列未启用 enclave** |**列未启用 enclave**| **列已启用 enclave**  |**列已启用 enclave** |
|:---|:---|:---|:---|:---|
| | **随机加密**  | **确定性加密**     | **随机加密**      | **确定性加密**     |
| **就地加密** | 不支持  | 不支持   | 是否支持         | 是否支持    |
| **相等比较**   | 不支持 | 支持（在 enclave 之外） | 支持（在 enclave 内） | 支持（在 enclave 之外） |
| **超出相等的比较运算符** | 不支持  | 不支持   | 是否支持      | 不支持     |
| **LIKE**    | 不支持      | 不支持    | 是否支持     | 不支持    |

就地加密包括对 enclave 内的以下操作的支持：

- 初始加密现有列中存储的数据。
- 重新加密列中的现有数据，例如：
  
  - 轮替列加密密钥（使用新密钥重新加密列）。
  - 更改加密类型。  

- 解密加密列中存储的数据（将该列转换为纯文本列）。

加密操作中涉及的列加密密钥（或密钥）必须已启用 enclave 才能使用就地加密：

- 初始加密：所加密的列的列加密密钥必须已启用 enclave。
- 重新加密：当前列加密密钥和目标列加密密钥（如果不同于当前密钥）都必须已启用 enclave。
- 解密：列的当前列加密密钥必须已启用 enclave。

## <a name="known-limitations"></a>已知的限制

一般限制： 

- 为[功能详细信息](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine#feature-details)中的当前 Always Encrypted 版本列出的所有限制也适用于具有安全 enclave 的 Always Encrypted（使用已启用 enclave 的密钥加密的列），通过添加对就地加密和富计算的支持而删除的限制除外。

- 相等比较保留了确定性加密支持的唯一 Transact-SQL 运算符，并且相等比较通过比较 enclave 之外的已加密文本值来执行，不管列加密密钥是否已启用 enclave。 通过确定性加密的已启用 enclave 的列加密密钥解锁的唯一新功能是就地加密操作。 如果具有使用确定性加密（以及未启用 enclave 的密钥）加密的列，则需要使用随机加密重新加密列才能启用富计算（模式匹配、比较操作）。

- 有关使用排序规则的现有限制适用于使用已启用 enclave 的列加密密钥加密的列：使用确定性加密加密的字符字符串列（char、nchar、varchar、nvarchar）必须使用排序顺序为 binary2 的排序规则（BIN2 排序规则）。 使用非 BIN2 排序规则的字符字符串列可以使用随机加密进行加密 – 但为此类列（如果它们使用已启用 enclave 的列加密密钥进行加密）启用的唯一新功能是就地加密。 若要支持富计算（模式匹配、比较操作），列必须使用 BIN2 排序规则  （并且必须使用随机加密和已启用 enclave 的列加密密钥加密列）。

- 不支持将已启用 enclave 的密钥用于内存中表中的列。

- 就地加密操作不能与列元数据的任何其他更改合并，排序规则和为 Null 性更改除外。 例如，不能加密、重新加密或解密列，也不能更改单个 ALTER TABLE 或 ALTER COLUMN Transact-SQL 语句中的列的数据类型。 需要使用两个单独的语句。

以下限制适用于当前预览版，但正在计划予以解决：

- 使用随机加密的已启用 enclave 的列无法编制索引，这意味着比较操作或 LIKE 操作需要进行表扫描。

- 支持具有安全 enclave 的 Always Encrypted 的唯一客户端驱动程序是 .NET Framework 4.7.2 中用于 SQL Server 的 .NET Framework 数据提供程序 (ADO.NET)。 没有 ODBC/JDBC 支持。

- 用于存储已启用 enclave 的列主密钥的唯一受支持密钥存储是 Windows 证书存储和 Azure 密钥保管库。

- 具有安全 enclave 的 Always Encrypted 的工具支持当前不完整。 若要通过 ALTER TABLE Transact-SQL 语句触发就地加密操作，需要使用 SSMS 中的查询窗口发出该语句，或者可以自行编写可发出该语句的程序。 SqlServer PowerShell 模块中的 Set-SqlColumnEncryption cmdlet 和 SQL Server Management Studio 中的 Always Encrypted 向导尚不支持就地加密 - 这两种工具当前将数据移出数据库以执行加密操作，即使用于这些操作的列加密密钥已启用 enclave 也是如此。 

## <a name="known-issues"></a>已知问题

- 针对非 UNICODE（char、varchar）字符串列的富计算要求在数据库级别设置 BIN2 排序规则。 请参阅[管理排序规则](configure-always-encrypted-enclaves.md#manage-collations)中有关非 UNICODE 字符串列的特殊注意事项。

## <a name="next-steps"></a>Next Steps

- 在 SSMS 中设置测试环境并尝试使用具有安全 enclave 的 Always Encrypted 功能，请参阅[教程：通过 SSMS 开始使用具有安全 enclave 的 Always Encrypted](../tutorial-getting-started-with-always-encrypted-enclaves.md)。
