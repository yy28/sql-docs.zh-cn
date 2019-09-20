---
ms.openlocfilehash: ccc96ecf7dccede236616e4680243116b8492d6b
ms.sourcegitcommit: 0c6c1555543daff23da9c395865dafd5bb996948
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2019
ms.locfileid: "70309857"
---
## <a name="enabled-deployment-scenarios"></a>启用的部署方案

SQL Server 2019 候选发布 (RC) 启用以下方案：

- 并行安装。 使用 SQL Server 2012 到 SQL Server 2017 的实例或 SQL Server 2019 CTP 3.0 或更高版本的其他实例，安装 SQL Server 2019 RC 的实例。
   >[!NOTE]
   >虽然 SQL Server 2008 和 2008 R2 不会阻止并行安装，但它们与 SQL Server 2019 之间并没有共同支持的 Windows 操作系统版本。
- 就地升级。 从 SQL Server 2012 到 SQL Server 2017 和 SQL Server CTP 3.0 的实例升级到 SQL Server 2019 RC。 不支持从低于 3.0 的 SQL Server 2019 CTP 进行升级，必须执行新的安装。
   >[!NOTE]
   >虽然不会阻止从 SQL Server 2008 和 2008 R2 进行就地升级，但它们与 SQL Server 2019 之间并没有共同支持的 Windows 操作系统版本。

## <a name="support"></a>支持

SQL Server 2019 RC 是预览版软件。 它未公开支持操作。 加入 [SQL 早期采用者计划](http://aka.ms/sqleap)的客户可能经与 Microsoft 磋商后，可按特殊协议运行 SQL Server 2019 RC。

对于未使用早期采用计划的客户，可在以下位置之一找到有限支持：

- 论坛
  - [SQL Server 入门](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqlgetstarted)
  - [Transact-SQL](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=transactsql)
  - [SQL Server 文档](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqldocumentation)

- 或使用 [#sqlhelp](https://twitter.com/search?q=%23sqlhelp) 发布推文 [@SQLServer](https://twitter.com/SQLServer)

试用 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]！ 

- [![从评估中心下载](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=862101) [下载 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 以在 Windows 上安装](https://go.microsoft.com/fwlink/?LinkID=862101)。
- 在 Linux 上针对 [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md)、[SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) 和 [Ubuntu](../linux/quickstart-install-connect-ubuntu.md) 安装。
- [在 Docker 上运行 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](../linux/quickstart-install-connect-docker.md)。
