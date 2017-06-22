---
title: "使用 SQL Server Management Studio 配置 Always Encrypted | Microsoft Docs"
ms.custom: 
ms.date: 11/30/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.PAGE.F1
- SQL13.SWB.COLUMNENCRYPTIONKEY.PAGE.F1
- SQL13.SWB.COLUMNMASTERKEY.ROTATION.F1
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 80c832db0ffdb9a3666b60a19fdf11a01750b2e1
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="configure-always-encrypted-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 配置 Always Encrypted
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

本文介绍使用 [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx) 配置始终加密和管理使用始终加密的数据库时所需执行的任务。

当你使用 SSMS 配置始终加密时，SSMS 会处理始终加密密钥和敏感数据，因此，这些密钥和数据会以纯文本形式显示在 SSMS 进程内。 因此，在安全的计算机上运行 SSMS 至关重要。 如果数据库托管在 SQL Server 中，请确保 SSMS 不是在托管 SQL Server 实例的计算机上运行，而是在另一台计算机上运行。 由于始终加密的主要目的是确保加密的敏感数据的安全（即使数据库系统遭到入侵），因此，在 SQL Server 计算机上执行 PowerShell 脚本来处理密钥或敏感数据会减少或抵消该功能带来的益处。 有关其他建议，请参阅 [密钥管理安全注意事项](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#SecurityForKeyManagement)。

SSMS 不支持管理数据库 (DBA) 的用户与管理加密密码并有权访问纯文本数据的用户（安全管理员和/或应用程序管理员）之间的角色分离。 如果你的组织强制实施角色分离，你应使用 PowerShell 来配置始终加密。 有关其他信息，请参阅 [Always Encrypted 密钥管理概述](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md) 和 [使用 PowerShell 配置 Always Encrypted](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)。

## <a name="configuring-always-encrypted-using-the-always-encrypted-wizard"></a>使用始终加密向导配置始终加密

[始终加密向导](../../../relational-databases/security/encryption/always-encrypted-wizard.md) 是一个功能强大的工具，可让你为所选数据库列设置所需的加密配置。 根据当前的始终加密配置和所需的目标配置，该向导可以对列加密或解密（删除加密），或重新对其加密（例如，使用为列配置的新列加密密钥或不同于当前类型的加密类型）。 可以在该向导的单次运行中配置多个列。

如果没有为始终加密预配任何密钥，该向导将自动为你生成密钥。 你只需为列主密钥选择密钥存储：Windows 证书存储或 Azure 密钥保管库。 该向导将自动为密钥生成名称并在数据库中为其生成元数据对象。 如果你需要更好地控制密钥预配方式（并对包含列主密钥的密钥存储有更多选择），可以使用“新建列主密钥”  和“新建列加密密钥”  对话框（如下所述）在启动该向导之前预配密钥。 然后就可以在始终加密向导中选择现有的列加密密钥。

有关如何使用该向导的详细信息，请参阅  [始终加密向导](../../../relational-databases/security/encryption/always-encrypted-wizard.md)。

## <a name="querying-encrypted-columns"></a>查询加密列

本部分介绍如何执行以下操作：   
-   检索存储在加密列中的密码文本值。   
-   检索存储在加密列中的纯文本值。   
-   发送针对加密列的纯文本值（例如，在 `INSERT` 或 `UPDATE` 声明中，以及作为 `WHERE` 声明中的 `SELECT` 字句的查找参数）。   

### <a name="retrieving-ciphertext-values-stored-in-encrypted-columns"></a>检索存储在加密列中的密码文本值    

从加密列中检索值作为密码文本（无需解密值）：
1.  请确保已为“查询编辑器”窗口（从中运行 `SELECT` 查询）的数据库连接禁用了 Always Encrypted。 请参阅下面的 [为数据库连接启用和禁用 Always Encrypted](#en-dis) 。      
2.  运行 `SELECT` 查询。 从加密列中检索到的任何数据都将作为二进制（加密）值返回。   

*示例*   
假定 `SSN` 是 `Patients` 表中的加密列，如果为数据库连接禁用了 Always Encrypted，则以下所示的查询将检索二进制密码文本值。   

![always-encrypted-ciphertext](../../../relational-databases/security/encryption/media/always-encrypted-ciphertext.png)
 
### <a name="retrieving-plaintext-values-stored-in-encrypted-columns"></a>检索存储在加密列中的纯文本值    

从加密列中检索值作为纯文本（用于解密值）：   
1.  请确保已为“查询编辑器”窗口（从中运行 `SELECT` 查询）的数据库连接启用了 Always Encrypted。 这将指示用于 SQL Server（ SSMS 使用）的 .NET Framework 数据提供程序对从加密列中检索到的数据进行解密。 请参阅下面的 [为数据库启用和禁用 Always Encrypted](#en-dis) 。
2.  请确保可以访问所有为加密列配置的列主密钥。 例如，如果列主密钥是证书，请确保在运行 SSMS 的计算机上部署此证书。 或者，如果列主密钥是存储在 Azure 密钥保管库中的密钥，请确保你有权访问此密钥，此外，可能会提示你登录到 Azure。
3.  运行 `SELECT` 查询。 从加密列中检索到的任何数据都将作为原始数据类型值以纯文本形式返回。   

*示例*   
假定 SSN 是 `char(11)` 表中的加密 `Patients` 列，如果为数据库连接启用了 Always Encrypted，并且你有权访问为 `SSN` 列配置的列主密钥，则以下所示的查询将返回纯文本值。   

![always-encrypted-plaintext](../../../relational-databases/security/encryption/media/always-encrypted-plaintext.png)
 
### <a name="sending-plaintext-values-targeting-encrypted-columns"></a>发送针对加密列的纯文本值       

执行发送针对加密列的值的查询，例如，通过存储在加密列中的值进行插入、更新或筛选的查询：   
1.  请确保已为“查询编辑器”窗口（从中运行 `SELECT` 查询）的数据库连接启用了 Always Encrypted。 这将指示用于 SQL Server 的 .NET Framework 数据提供程序（用于 SSMS）对针对加密列的参数化 Transact-SQL 变量（见下文）进行加密。 请参阅下面的 [为数据库启用和禁用 Always Encrypted](#en-dis) 。   
2.  请确保可以访问所有为加密列配置的列主密钥。 例如，如果列主密钥是证书，请确保在运行 SSMS 的计算机上部署此证书。 或者，如果列主密钥是存储在 Azure 密钥保管库中的密钥，请确保你有权访问此密钥，此外，可能会提示你登录到 Azure。   
3.  请确保已为“查询编辑器”窗口启用 Always Encrypted 参数化。 （要求至少为 SSMS 版本 17.0。）声明 Transact-SQL 变量，并使用要发送到数据库的值对其进行初始化，以使用该值进行插入、更新或筛选。 有关详细信息，请参阅下面的 [Always Encrypted 参数化](#param)。   
    >   [!NOTE]
    >   Always Encrypted 支持有限子网的类型转换，在许多情况下，Transact-SQL 变量的数据类型都要求与其针对的目标数据库列的类型相同。   
4.  运行查询，将 Transact-SQL 变量的值发送到数据库。 SSMS 会将变量转换为查询参数并对其值进行加密，然后再将加密值发送到数据库。   

*示例*   
假定 `SSN` 是 `char(11)` 表中的加密 `Patients` 列，如果已为数据库连接启用 Always Encrypted，为“查询编辑器”窗口启用了 Always Encrypted 参数化，并且你有权访问为 `'795-73-9838'` 列配置的列主密钥，则下面的脚本将尝试在 SSN 列中查找包含 `LastName` 的行并返回 `SSN` 列的值。   

![always-encrypted-patients](../../../relational-databases/security/encryption/media/always-encrypted-patients.png)
 
### <a name="en-dis"></a> Enabling and disabling Always Encrypted for a database connection   

为数据库连接启用 Always Encrypted 将指示用于 SQL Server 的 .NET Framework 数据提供程序（用于 SQL Server Management Studio）以透明方式尝试以下操作：   
-   对从加密列中检索到的并在查询结果中返回的任何值进行解密。   
-   对针对加密数据库的参数化 Transact-SQL 变量的值进行加密。   
若要为数据库连接启用 Always Encrypted，请在“连接到服务器” `Column Encryption Setting=Enabled`**对话框的“其他属性”****选项卡中指定** 。    
若要为数据库连接禁用 Always Encrypted，请指定 `Column Encryption Setting=Disabled` ，或者从“连接到服务器”  对话框（其默认值为“禁用”  ）的“其他属性”  选项卡中删除“列加密设置” 的设置。   

>  [!TIP] 
>  在为现有“查询编辑器”窗口启用和禁用 Always Encrypted 之间进行切换：   
>  1.   右键单击“查询编辑器”窗口中的任意位置。
>  2.   选择“连接” > “更改连接…”， 
>  3.   单击“选项”>>，
>  4.   选中“其他属性”选项卡，然后键入 `Column Encryption Setting=Enabled` 以启用 Always Encrypted 行为或删除该设置以禁用 Always Encrypted 行为。   
>  5.   单击 **“连接”**。   
   
### <a name="param"></a>Parameterization for Always Encrypted   
 
Always Encrypted 参数化是 SQL Server Management Studio 中的一种功能，可自动将 Transact-SQL 变量转换为查询参数（[SqlParameter 类](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)的实例）。 （要求至少为 SSMS 版本 17.0。）这允许用于 SQL Server 的基础 .NET Framework 数据提供程序对针对加密列的数据进行检测，并在将数据发送到数据库之前对其进行加密。 
  
如果没有进行参数化，.NET Framework 数据提供程序会传递你在“查询编辑器”中编写的每个声明，作为非参数化查询。 如果查询包含文字或针对加密列的 Transact-SQL 变量，用于 SQL Server 的 .NET Framework 数据提供程序将无法在将查询发送到数据库之前，对它们进行检测和加密。 结果由于纯文本文字 Transact-SQL 变量和加密列之间的类型不匹配，查询将失败。 例如，假定 `SSN` 列已加密，如果没有参数化，以下查询将失败。   

```tsql
DECLARE @SSN NCHAR(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN
```

#### <a name="enablingdisabling-parameterization-for-always-encrypted"></a>启用/禁用 Always Encrypted 参数化   


默认情况下，将禁用 Always Encrypted。    

为当前的“查询编辑器”窗口启用/禁用 Always Encrypted 参数化：   
1.  在主菜单中，选择“查询”  。   
2.  选择“查询选项…”。   
3.  导航到“执行” > “高级”。   
4.  选择或取消选择“启用 Always Encrypted 参数化”。   
5.  单击 **“确定”**。   

为以后的“查询编辑器”窗口启用/禁用 Always Encrypted 参数化：   
1.  在主菜单中，选择“工具”  。   
2.  选择“选项…”。   
3.  导航到“查询执行” > “SQL Server” > “高级”。   
4.  选择或取消选择“启用 Always Encrypted 参数化”。   
5.  单击 **“确定”**。   

如果在使用启用了 Always Encrypted 的数据库连接的“查询编辑器”窗口中执行查询，但是没有为“查询编辑器”窗口启用参数化，系统将提示你启用它。   
>   [!NOTE]   
>   Always Encrypted 参数化仅在使用启用了 Always Encrypted 的数据库连接的“查询编辑器”窗口中有效（请参阅 [为数据库启用和禁用 Always Encrypted](#en-dis)）。 如果“查询编辑器”窗口使用未启用 Always Encrypted 的数据库连接，则不会对 Transact-SQL 变量进行参数化。   

#### <a name="how-parameterization-for-always-encrypted-works"></a>Always Encrypted 参数化的工作方式   

如果在数据库连接中同时为“查询编辑器”窗口启用了 Always Encrypted 参数化和 Always Encrypted 行为，SQL Server Management Studio 将尝试对符合以下先决条件的 Transact-SQL 变量进行参数化：    
- 在同一语句中进行声明和初始化（内联初始化）。 使用单独的 `SET` 语句进行声明的变量将不会进行参数化。   
- 使用单个文字进行初始化。 使用包含任何运算符或函数的表达式进行初始化的变量将不会进行参数化。      

下面是 SQL Server Management Studio 将对其进行参数化的变量的示例。   
```tsql
DECLARE @SSN char(11) = '795-73-9838';
   
DECLARE @BirthDate date = '19990104';
DECLARE @Salary money = $30000;
```

而此处是几个 SQL Server Management Studio 将不会尝试对其进行参数化的变量的示例：   
```tsql
DECLARE @Name nvarchar(50); --Initialization seperate from declaration
SET @Name = 'Abel';
   
DECLARE @StartDate date = GETDATE(); -- a function used instead of a literal
   
DECLARE @NewSalary money = @Salary * 1.1; -- an expression used instead of a literal
```
 
为了成功完成尝试的参数化操作：   
- 用于要参数化的变量初始化的文字类型必须与变量声明中的类型匹配。   
- 如果变量的声明类型是日期类型或时间类型，变量必须通过使用以下 ISO 8601 标准格式之一的字符串进行初始化。   

下面是会导致参数化错误的 Transact-SQL 变量声明的示例：   
```tsql
DECLARE @BirthDate date = '01/04/1999' -- unsupported date format   
   
DECLARE @Number int = 1.1 -- the type of the literal does not match the type of the variable   
```
SQL Server Management Studio 使用 Intellisense 来通知你哪些参数可成功进行参数化而哪些参数化尝试会失败（及其原因）。   

可成功进行参数化的变量的声明将在“查询编辑器”中使用警告下划线进行标记。 如果将鼠标悬停在带有警告下划线标记的声明语句上，将显示参数化过程的结果，其中包括生成的 [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) 对象（该变量的映射对象）的键属性值： [SqlDbType](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqldbtype.aspx)、 [Size](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.size.aspx)、 [Precision](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.precision.aspx)、 [Scale](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.scale.aspx)、 [SqlValue](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqlvalue.aspx)。 还会在“错误列表”  视图的“警告”  选项卡中，显示已成功进行参数化的所有变量的完整列表。 若要打开“错误列表”  视图，请在主菜单中选择“视图”  ，然后选择“错误列表” 。    

如果 SQL Server Management Studio 已尝试对变量进行参数化，但是参数化操作失败，那么变量的声明将以错误下划线进行标记。 如果将鼠标悬停在带有错误下划线标记的声明语句上，可获得有关该错误的结果。 还会在“错误列表”  视图的“错误”  选项卡中，显示所有变量的参数化错误的完整列表。 若要打开“错误列表”  视图，请在主菜单中选择“视图”  ，然后选择“错误列表” 。   

下面的屏幕截图介绍的是具有六个变量声明的示例。 SQL Server Management Studio 已成功对前三个变量进行了参数化。 最后三个变量不符合参数化的先决条件，因此，SQL Server Management Studio 不会尝试对其进行参数化（其声明不会以任何方式标记）。   

![always-encrypted-parameter-warnings](../../../relational-databases/security/encryption/media/always-encrypted-parameter-warnings.png)
 
下面是另一个示例，介绍了两个符合参数化的先决条件的变量，但是参数化尝试失败，因为变量未正确进行初始化。    
 
![always-encrypted-error](../../../relational-databases/security/encryption/media/always-encrypted-error.png)
 
>   [!NOTE]
>   Always Encrypted 支持有限子网的类型转换，在许多情况下，Transact-SQL 变量的数据类型都要求与其针对的目标数据库列的类型相同。 例如，假定 `SSN` 表中的 `Patients` 列是 `char(11)`，以下查询将失败，因为 `@SSN` 变量的类型为 `nchar(11)`，与列的类型不匹配。   

```tsql
DECLARE @SSN nchar(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN;
```

    Msg 402, Level 16, State 2, Line 5   
    The data types char(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') collation_name = 'Latin1_General_BIN2' 
    and nchar(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') are incompatible in the equal to operator.

>   [!NOTE]
>   如果没有进行参数化，整个查询（包括类型转换）将在 SQL Server/Azure SQL 数据库内进行处理。 如果启用了参数化，某些类型转换将由 SQL Server Management Studio 中的 .NET Framework 来执行。 由于 .NET Framework 类型系统和 SQL Server 类型系统之间存在差异（例如某些类型的精度不同，如 float），启用了参数化来执行的查询可产生不同于未启用参数化来执行的查询的结果。 

#### <a name="permissions"></a>Permissions      

若要对加密列运行任何查询（包括在加密文本中检索数据的查询），则需要具有数据库中的 `VIEW ANY COLUMN MASTER KEY DEFINITION` 和 `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` 权限。   
若要对任何查询结果进行解密或对任何查询参数（通过对 Transact-SQL 变量进行参数化而生成）进行加密，除了上述权限，还需具有访问保护目标列的列主密钥的权限：   
- **证书存储 – 本地计算机** — 必须对用作列主密钥的证书具有 `Read` 访问权限，或必须是计算机上的管理员。   
- **Azure 密钥保管库** — 需要包含列主密钥的保管库上的 `get`、 `unwrapKey`和 verify 权限。   
- **密钥存储提供程序 (CNG)** 使用密钥存储或密钥时，可能会提示你提供必要的权限和凭据，具体取决于存储和 KSP 配置。   
- **加密服务提供程序 (CAPI)** — 使用密钥存储或密钥时，可能会提示你提供必要的权限和凭据，具体取决于存储和 CSP 配置。   

有关详细信息，请参阅 [创建并存储列主密钥 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。


<a name="provisioncmk"></a>
## <a name="provisioning-column-master-keys-new-column-master-key"></a>预配列主密钥（新建列主密钥）

“新建列主密钥”对话框允许你生成列主密钥或选择密钥存储中的现有密钥，并在数据库中为所创建或所选择的密钥创建列主密钥元数据。

1.  使用**对象资源管理器**导航到数据库下面的“安全”>“始终加密密钥”文件夹。
2.  右键单击“列主密钥”文件夹，然后选择“新建列主密钥...”。 
3.  在“新建列主密钥”  对话框中，输入列主密钥元数据对象的名称。
4.  选择密钥存储：
    - **证书存储 – 当前用户** — 指示当前用户证书存储在 Windows 证书存储中的位置，这是你的个人存储。 
    - **证书存储 — 本地计算机** — 指示本地计算机证书存储在 Windows 证书存储中的位置。 
    - **Azure 密钥保管库** — 需要登录到 Azure（单击“登录” ）。 一旦登录，就可以选择你的 Azure 订阅之一和密钥保管库。
    - **密钥存储提供程序(CNG)** — 指示可通过实现下一代加密技术 (CNG) API 的密钥存储提供程序 (KSP) 访问的密钥存储。 通常，这种存储是硬件安全模块 (HSM)。 选择此选项后，将需要选择 KSP。 “Microsoft 软件密钥存储提供程序” 默认处于选中状态。 如果你想使用存储在 HSM 中的列主密钥，请为设备选择 KSP（必须在打开该对话框之前在计算机上安装并配置 KSP）。
    -   **加密服务提供程序(CAPI)** — 可以通过实现加密 API (CAPI) 的加密服务提供程序 (CSP) 访问的密钥存储。 通常，这种存储是硬件安全模块 (HSM)。 选择此选项后，将需要选择 CSP。  如果你想使用存储在 HSM 中的列主密钥，请为设备选择 CSP（必须在打开该对话框之前在计算机上安装并配置 CSP）。
    
    >   [!NOTE]
    >   由于 CAPI 是已弃用的 API，因此，“加密服务提供程序(CAPI)”选项默认处于禁用状态。 你可以通过在 Windows 注册表中的 **[HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\sql13\Tools\Client\Always Encrypted]** 项下面创建“已启用 CAPI 提供程序”DWORD 值并将其设置为 1，来启用该选项。 应使用 CNG 而不是 CAPI，除非密钥存储不支持 CNG。
   
    有关上述密钥存储的详细信息，请参阅 [创建并存储列主密钥 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

5.  选择密钥存储中的现有密钥，或者单击“生成密钥”  或“生成证书”  按钮，在密钥存储中创建一个密钥。 
6.  单击“确定”  ，新密钥随即显示在列表中。 

SQL Server Management Studio 将在数据库中为列主密钥创建元数据。 该对话框通过生成并发出 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 语句来实现此操作。


<a name="provisioncek"></a> 
## <a name="provisioning-column-encryption-keys-new-column-encryption-key"></a>预配列加密密钥（新建列加密密钥）

“新建列加密密钥”  对话框允许生成列加密密钥、使用列主密钥对其加密，以及在数据库中创建列加密密钥元数据。

1.  使用 **对象资源管理器**导航到数据库下面的“安全”/“始终加密密钥”  文件夹。
2.  右键单击“列加密密钥”  文件夹，然后选择“新建列加密密钥...” 。 
3.  在“新建列加密密钥”  对话框中，输入列加密密钥元数据对象的名称。
4.  在数据库中选择一个表示列主密钥的元数据对象。
5.  单击 **“确定”**。 


SQL Server Management Studio 将生成新的列加密密钥，然后它将从数据库中检索所选列主密钥的元数据。 然后，SQL Server Management Studio 将使用该列主密钥元数据访问包含列主密钥的密钥存储并对列加密密钥加密。 最后，将在数据库中为新的列加密密钥创建元数据。 该对话框通过生成并发出 [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) 语句来实现此操作。

### <a name="permissions"></a>Permissions

需要数据库中的 *更改任意加密主密钥* 和 *查看任意列主密钥定义* 数据库权限，该对话框才能创建列加密密钥元数据和访问列主密钥元数据。
若要访问密钥存储并使用列主密钥，可能需要密钥存储或/和密钥上的权限：
- **证书存储 – 本地计算机** — 必须对用作列主密钥的证书具有读取访问权限，或者是计算机上的管理员。
- **Azure 密钥保管库** — 需要包含列主密钥的保管库上的 *get*、 *unwrapKey*、 *wrapKey*、 *sign*和 *verify*  权限。
- **密钥存储提供程序(CNG)** — 使用密钥存储或密钥时可能提示你提供必要的权限和凭据，具体取决于存储和 KSP 配置。
- **加密服务提供程序(CAPI)** — 使用密钥存储或密钥时可能提示你提供必要的权限和凭据，具体取决于存储和 CSP 配置。

有关详细信息，请参阅 [创建并存储列主密钥 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

<a name="rotatecmk"></a>
## <a name="rotating-column-master-keys"></a>轮替列主密钥

列主密钥轮替是将现有列主密钥替换为新列主密钥的过程。 如果密钥已泄漏，或者为了遵守强制规定必须定期轮换加密密钥的组织的策略或遵从性规则，则可能需要轮换密钥。 列主密钥轮替包括对使用当前列主密钥保护的列加密密钥解密，使用新的列主密钥对其重新加密，以及更新密钥元数据。 有关详细信息，请参阅 [Always Encrypted 密钥管理概述](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。

**步骤 1：预配新的列主密钥**

按照上面“预配列主密钥”一节中的步骤预配新的列主密钥。

**步骤 2：使用新的列主密钥加密列加密密钥**

一个列主密钥通常保护一个或多个列加密密钥。 每个列加密密钥在数据库中存储有一个加密值，这是使用列主密钥加密列加密密钥的产物。
在此步骤中，使用新的列主密钥，来加密使用你要轮替的列主密钥保护的每个列加密密钥，然后在数据库中存储新的加密值。 因此，受轮替影响的每个列加密密钥有两个加密值：一个值是使用现有列主密钥加密的，一个新值是使用新的列主密钥加密的。

1.  使用**对象资源管理器**导航到“安全”/“始终加密密钥”/“列主密钥”文件夹并找到要轮替的列主密钥。
2.  右键单击该列主密钥并选择“轮替”。
3.  在“列主密钥轮替”对话框的“目标”字段中，选择在步骤 1 中创建的新列主密钥的名称。
4.  查看现有列主密钥保护的列加密密钥的列表。 这些密钥将受到轮转的影响。
5.  单击 **“确定”**。

SQL Server Management Studio 将获取使用旧列主密钥保护的列加密密钥的元数据，以及旧列主密钥和新列主密钥的元数据。 然后，SSMS 将使用列主密钥元数据来访问包含旧列主密钥的密钥存储并对列加密密钥解密。 随后，SSMS 将访问包含新列主密钥的密钥存储，以生成一组新的列加密密钥加密值，然后它会将新值添加到元数据中（生成并发出 [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) 语句）。

> [!NOTE]
> 请确保使用旧列主密钥加密的每个列加密密钥未使用其他任何列主密钥进行加密。 换而言之，受轮转影响的每个列加密密钥在数据库中必须恰好有一个加密值。 如果受影响的任何列加密密钥具有多个加密值，则需要删除值，然后才能继续轮替（有关如何删除列加密密钥的加密值，请参阅 *步骤 4* ）。

**步骤 3：使用新的列主密钥配置应用程序**

在此步骤中，你需要确保查询使用所要轮替的列主密钥保护的数据库列（即，使用所要轮替的列主密钥加密的列加密密钥加密的数据库列）的所有客户端应用程序能够访问新的列主密钥。 此步骤取决于新列主密钥所在密钥存储的类型。 例如：
- 如果新列主密钥是存储在 Windows 证书存储中的证书，则需要将该证书部署到数据库中由列主密钥的密钥路径指定的同一个证书存储位置（“当前用户” 或“本地计算机” ）。 该应用程序需要能够访问该证书：
    - 如果该证书存储在“当前用户”证书存储位置中，则需要将该证书导入到应用程序的 Windows 标识（用户）的“当前用户”存储中。 
    - 如果该证书存储在“本地计算机”证书存储位置中，则应用程序的 Windows 标识必须有权访问该证书。 
- 如果新的列主密钥存储在 Microsoft Azure 密钥保管库中，则必须实现应用程序，以便它可以在 Azure 中进行身份验证并有权访问该密钥。

有关详细信息，请参阅 [创建并存储列主密钥 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

> [!NOTE]
> 在轮替的这一阶段，旧列主密钥和新列主密钥均有效并可用于访问数据。

**步骤 4：清理使用旧列主密钥加密的列加密密钥值**

将所有应用程序配置为使用新的列主密钥后，请从数据库中删除使用 *旧* 列主密钥加密的列加密密钥值。 删除旧值可确保随时能够进行下一次轮替（请记住，使用要轮替的列主密钥保护的每个列加密密钥必须恰好有一个加密值）。

在存档或删除旧列主密钥之前清理旧值的另一个原因与性能相关：在查询加密列时，启用始终加密的客户端驱动程序可能需要尝试解密两个值：旧值和新值。 该驱动程序不知道在这两个列主密钥中，哪个密钥在应用程序的环境中有效，因此它会从服务器中同时检索这两个密钥的加密值。 如果解密其中一个值失败（因为该值是使用不可用的列主密钥保护的，例如，该密钥是已从存储中删除的旧列主密钥），驱动程序将尝试使用新的列主密钥来解密另一个值。

> [!WARNING]
> 如果你在列加密密钥的对应列主密钥可供应用程序使用之前删除列加密密钥的值，应用程序将再也无法对数据库列解密。

1.  使用**对象资源管理器**导航到“安全”>“始终加密密钥”文件夹并找到要替换的现有列主密钥。
2.  右键单击现有的列主密钥，然后选择“清理”。
3.  查看要删除的列加密密钥值列表。
4.  单击 **“确定”**。

SQL Server Management Studio 将发出 [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) 语句，以删除用旧列主密钥加密的列加密密钥的加密值。

**步骤 5：删除旧的列主密钥的元数据**

如果你选择从数据库中删除旧列主密钥的定义，可使用以下步骤。 
1.  使用**对象资源管理器**导航到“安全”>“始终加密密钥”>“列主密钥”文件夹，并找到要从数据库中删除的旧列主密钥。
2.  右键单击旧列主密钥，然后选择“删除”。 （这将生成并发出 [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md) 语句，以删除列主密钥元数据。）
3.  单击 **“确定”**。

> [!NOTE]
> 强烈建议你不要在轮换后永久地删除旧的列主密钥。 相反，应该在其当前密钥存储中保留旧的列主密钥，或将其存档在另一个安全位置。 如果在配置新的列主密钥之前，从备份文件将数据库还原到某个时间点，则需要使用旧密钥来访问数据。

### <a name="permissions"></a>Permissions

轮替列主密钥要求具备以下数据库权限：

- **更改任意列主密钥** — 在为新列主密钥创建元数据以及删除旧列主密钥的元数据时需要。
- **更改任意列加密密钥** — 在修改列加密密钥元数据（添加新的加密值）时需要。
- **查看任意列主密钥定义** —在访问和读取列主密钥的元数据时需要。
- **查看任意列加密密钥定义** —在访问和读取列加密密钥的元数据时需要。 

你还需要能够访问密钥存储中的旧列主密钥和新列主密钥。 若要访问密钥存储并使用列主密钥，可能需要密钥存储或/和密钥上的权限：
- **证书存储 – 本地计算机** — 必须对用作列主密钥的证书具有读取访问权限，或者是计算机上的管理员。
- **Azure 密钥保管库** — 需要包含列主密钥的保管库上的 *create*、 *get*、 *unwrapKey*、 *wrapKey*、 *sign*和 *verify* 权限。
- **密钥存储提供程序(CNG)** — 使用密钥存储或密钥时可能提示你提供必要的权限和凭据，具体取决于存储和 KSP 配置。
- **加密服务提供程序(CAPI)** — 使用密钥存储或密钥时可能提示你提供必要的权限和凭据，具体取决于存储和 CSP 配置。

有关详细信息，请参阅 [创建并存储列主密钥 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

<a name="rotatecek"></a> 
## <a name="rotating-column-encryption-keys"></a>轮替列加密密钥

轮替列加密密钥包括对使用要轮替掉的密钥进行加密的所有列中的数据进行解密，并使用新的列加密密钥对数据重新加密。

>[!NOTE]
> 如果包含列（使用要轮替的密钥加密）的表较大，则轮替列加密密钥可能需要很长时间。 对数据重新加密时，应用程序无法写入到受影响的表。 因此，组织需要非常谨慎地计划列加密密钥轮替。
若要轮替列加密密钥，请使用始终加密向导。

1.  为数据库打开该向导：右键单击数据库，指向“任务”，然后单击“加密列”。
2.  查看“简介”页，然后单击“下一步”。
3.  在“列选择”页上，展开表并找到你要替换的所有列，这些列当前使用旧的列加密密钥加密。
4.  对于使用旧的列加密密钥加密的每个列，将“加密密钥”  设置为自动生成的新密钥。 **注意：** 或者，你也可以在运行该向导之前创建新的列加密密钥 — 请参阅上面的 *预配列加密密钥* 一节。
5.  在“主密钥配置”  页上，选择一个位置来存储新密钥，并选择主密钥源，然后单击“下一步” 。 **注意：**如果你使用的是现有的列加密密钥（不是自动生成的密钥），则无需在此页面上执行任何操作。
6.  在“验证”页上，选择是要立即运行脚本还是创建 PowerShell 脚本，然后单击“下一步”。
7.  在“摘要”页上，查看你选择的选项，单击“完成”，并在完成后关闭该向导。
8.  使用**对象资源管理器**导航到“安全”/“始终加密密钥”/“列加密密钥”文件夹，并找到要从数据库中删除的旧列加密密钥。 右键单击该密钥，然后选择“删除” 。

### <a name="permissions"></a>Permissions

轮替列加密密钥需要以下数据库权限： **更改任意列主密钥** — 在使用自动生成的新列加密密钥（还将生成新的列主密钥及其新的元数据）时需要。
**更改任意列加密密钥** — 在为新列加密密钥添加元数据时需要。
**查看任意列主密钥定义** —在访问和读取列主密钥的元数据时需要。
**查看任意列加密密钥定义** —在访问和读取列加密密钥的元数据时需要。

你还需要能够访问新列加密密钥和旧列加密密钥的列主密钥。 若要访问密钥存储并使用列主密钥，可能需要密钥存储或/和密钥上的权限：
- **证书存储 – 本地计算机** — 必须对用作列主密钥的证书具有读取访问权限，或者是计算机上的管理员。
- **Azure 密钥保管库** — 需要包含列主密钥的保管库上的 get、unwrapKey 和 verify 权限。
- **密钥存储提供程序(CNG)** — 使用密钥存储或密钥时可能提示你提供必要的权限和凭据，具体取决于存储和 KSP 配置。
- **加密服务提供程序(CAPI)** — 使用密钥存储或密钥时可能提示你提供必要的权限和凭据，具体取决于存储和 CSP 配置。

有关详细信息，请参阅 [创建并存储列主密钥 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

## <a name="performing-dac-upgrade-operations-when-database-or-dacpac-uses-always-encrypted"></a>在数据库或 DACPAC 使用始终加密时执行 DAC 升级操作

具有包含加密列的架构的 DACPAC 文件和数据库支持[DAC 操作](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3) 。 执行 DAC 升级操作时有一些特殊的注意事项 — 请参阅 [升级数据层应用程序](../../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md) 了解如何在各种工具（包括 SSMS）中执行 DAC 升级操作。 

当使用 DACPAC 升级数据库，并且 DACPAC 或目标数据库有加密列时，如果满足以下所有条件，升级操作将触发数据加密操作：
- 数据库包含一个具有数据的列。
- DACPAC 中存在相同的列。
- 数据库中的列的加密配置不同于 DACPAC 中相应列的配置。 请参阅下表了解详细信息。

| 条件|操作|
|:---|:---|
|列已在 DACPAC 中加密，但未在数据库中加密。| 将加密该列中的数据。|
|列未在 DACPAC 中加密，但已在数据库中加密。| 将解密该列中的数据（将为该列删除加密）。|
| 列在 DACPAC 和数据库中均已加密，但 DACPAC 中的列所使用的加密类型或/和列加密密钥与数据库中的相应列不同。|将解密该列中的数据，然后重新加密，以匹配 DACPAC 中的加密配置。|

> [!NOTE]
> 如果为数据库或 DACPAC 中的列配置的列主密钥存储在 Azure 密钥保管库中，系统将提示你登录到 Azure（如果尚未登录）。

### <a name="permissions"></a>Permissions

若要在 DACPAC 或目标数据库中设置了始终加密的情况下执行 DAC 升级操作，则可能需要以下部分或所有权限，具体取决于 DACPAC 中的架构与目标数据库架构之间的差异。

*更改任意列主密钥密钥*、 *更改任意列加密密钥*、 *查看任意列主密钥定义*、 *查看任意列加密密钥定义*

如果升级操作触发数据加密操作，则还需要能够访问为受影响的列配置的列主密钥：
- **证书存储 – 本地计算机** — 必须对用作列主密钥的证书具有读取访问权限，或者是计算机上的管理员。
- **Azure 密钥保管库** — 需要包含列主密钥的保管库上的 *create*、 *get*、 *unwrapKey*、 *wrapKey*、 *sign*和 *verify* 权限。
- **密钥存储提供程序(CNG)** — 使用密钥存储或密钥时可能提示你提供必要的权限和凭据，具体取决于存储和 KSP 配置。
- **加密服务提供程序(CAPI)** — 使用密钥存储或密钥时可能提示你提供必要的权限和凭据，具体取决于存储和 CSP 配置。

有关详细信息，请参阅 [创建并存储列主密钥 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

## <a name="migrating-databases-with-encrypted-columns-using-bacpac"></a>使用 BACPAC 迁移包含加密列的数据库

导出数据库时，系统将检索加密列中存储的所有数据并将其放入生成的 [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) 中（以加密形式）。 生成的 BACPAC 还包含始终加密密钥的元数据。

将 BACPAC 导入数据库时，BACPAC 中的加密数据将加载到数据库中，并将重新创建始终加密密钥元数据。

如果你的应用程序配置为修改或检索存储在源数据库（导出的数据库）中的加密数据，则无需执行任何特殊操作便可让应用程序查询目标数据库中的加密数据，因为这两个数据库中的密钥相同。


### <a name="permissions"></a>Permissions

你需要源数据库上的 *更改任意列主密钥* 和 *更改任意列加密密钥* 。 你需要目标数据库上的 *更改任意列主密钥*、 *更改任意列加密密钥*、 *查看任意列主密钥定义*和 *查看任意列加密* 。

## <a name="migrating-databases-with-encrypted-columns-using-sql-server-import-and-export-wizard"></a>使用 SQL Server 导入和导出向导迁移包含加密列的数据库

与使用 BACPAC 文件相比， [SQL Server 导入和导出向导](~/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md) 让你可以在数据迁移期间更好地控制存储在加密列中的数据的处理方式。

- 如果数据源是一个使用始终加密的数据库，则可以配置数据源连接，以便在导出操作期间对加密列中存储的数据解密，或使其保持加密状态。
- 如果你的数据目标是使用始终加密的数据库，则可以配置数据目标连接，以便对面向加密列的数据加密。

若要启用解密（针对数据源）或加密（针对数据目标），需要将数据源/目标连接配置为使用 [用于 SQL Server 的 .Net Framework 数据提供程序](https://msdn.microsoft.com/library/system.data.sqlclient.aspx) ，并且需要将“列加密设置”连接字符串关键字设置为“已启用” 。

下表列出了可能的迁移方案以及它们如何与始终加密以及每个连接的数据源和数据目标配置相关。

| 应用场景|源连接配置| 目标连接配置
|:---|:---|:---
|在迁移时加密数据（数据以纯文本形式存储在数据源中，并迁移到数据目标中的加密列）。| 数据提供程序/驱动程序： *任意*<br><br>列加密设置 = 已禁用<br><br>（如果使用用于 SQL Server 的 .Net Framework 数据提供程序和 .NET Framework 4.6 或更高版本。） | 数据提供程序/驱动程序： *用于 SQL Server 的 .Net Framework 数据提供程序* （需要 .NET Framework 4.6 或更高版本）<br><br>列加密设置 = 已启用
| 在迁移时解密数据（数据存储在数据源的加密列中，并以纯文本形式迁移到数据目标；如果数据目标是一个数据库，则不会加密目标列）。<br><br>**注意：** 在迁移之前，必须存在包含加密列的目标表。|数据提供程序/驱动程序： *用于 SQL Server 的 .Net Framework 数据提供程序* （需要 .NET Framework 4.6 或更高版本）<br><br>列加密设置=已启用|数据提供程序/驱动程序： *任意*<br><br>列加密设置 = 已禁用<br><br>（如果使用用于 SQL Server 的 .Net Framework 数据提供程序和 .NET Framework 4.6 或更高版本。）
|在迁移时重新加密数据（数据存储在数据源的加密列中，并以纯文本形式迁移到数据目标中使用不同加密类型的列加密密钥的列）。<br><br>**注意：** 在迁移之前，必须存在包含加密列的目标表。| 数据提供程序/驱动程序： *用于 SQL Server 的 .Net Framework 数据提供程序* （需要 .NET Framework 4.6 或更高版本）<br><br>列加密设置=已启用|数据提供程序/驱动程序： *用于 SQL Server 的 .Net Framework 数据提供程序* （需要 .NET Framework 4.6 或更高版本）<br><br>列加密设置=已启用
|移动加密数据而不对其解密。<br><br>**注意：** 在迁移之前，必须存在包含加密列的目标表。| 数据提供程序/驱动程序： *任意*<br>列加密设置 = 已禁用<br><br>（如果使用用于 SQL Server 的 .Net Framework 数据提供程序和 .NET Framework 4.6 或更高版本。）| 数据提供程序/驱动程序： *任意*<br>列加密设置 = 已禁用<br><br>（如果使用用于 SQL Server 的 .Net Framework 数据提供程序和 .NET Framework 4.6 或更高版本。）<br><br>用户必须将 ALLOW_ENCRYPTED_VALUE_MODIFICATIONS 设置为 ON。<br><br>有关详细信息，请参阅 [迁移通过“始终加密”保护的敏感数据](../../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)。


### <a name="permissions"></a>Permissions

若要 **加密** 或 **解密** 数据源中存储的数据，需要源数据库中的 *查看任意列主密钥定义* 和 *查看任意列加密密钥定义* 权限。

还需要能够访问为存储已加密数据或待解密数据的列配置的列主密钥：
- **证书存储 – 本地计算机** — 必须对用作列主密钥的证书具有读取访问权限，或者是计算机上的管理员。
- **Azure 密钥保管库** — 需要包含列主密钥的保管库上的 get、unwrapKey、wrapKey、sign 和 verify 权限。
- **密钥存储提供程序(CNG)** — 使用密钥存储或密钥时可能提示你提供的必要权限和凭据取决于存储和 KSP 配置。
- **加密服务提供程序(CAPI)** — 使用密钥存储或密钥时可能提示你提供的必要权限和凭据取决于存储和 CSP 配置。
有关详细信息，请参阅 [创建并存储列主密钥 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

## <a name="see-also"></a>另请参阅
- [Always Encrypted（数据库引擎）](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted 向导](../../../relational-databases/security/encryption/always-encrypted-wizard.md)
- [Always Encrypted 密钥管理概述](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [创建并存储列主密钥 (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [Always Encrypted（客户端开发）](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)
- [使用 PowerShell 配置 Always Encrypted](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)













