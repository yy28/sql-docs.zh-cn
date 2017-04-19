---
title: "使用 sqlBindR.exe 升级 R Services 的实例 | Microsoft Docs"
ms.custom: 
ms.date: 03/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016 CTP3)
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 20bac3263e709d6232aa6ebd062c6512a898e59e
ms.lasthandoff: 04/11/2017

---
# <a name="use-sqlbindrexe-to-upgrade-an-instance-of-r-services"></a>使用 sqlBindR.exe 升级 R Services 的实例
如果你安装了最新版本的 Microsoft R Server for Windows，则可以使用所包括的 **SqlBindR.exe** 工具来升级与 R Services 的实例关联的 R 组件。 此过程称为“绑定”，因为它会将 R Server 和 SQL Server R Services 的支持模型更改为使用新的 Modern Lifecycle 策略。 SQL Server 数据库的支持模型不会因此而更改。

一般情况下，此许可系统可确保数据科学家始终使用 R 的最新版本。有关 Modern Lifecycle 策略的条款的详细信息，请参阅 [Microsoft R Server 的支持时间线](https://msdn.microsoft.com/microsoft-r/rserver-servicing-support)。

绑定实例时，会发生几件事情：
+ R Server 和 SQL Server R Services 的支持策略从 SQL Server 2016 支持策略更改为新的 Modern Lifecycle 策略。
+ 通过当前由新的 Modern Lifecycle 策略管辖的 R Server 版本中的锁定步骤，与该实例关联的 R 组件将随每个版本自动升级。 
+ 将添加 R Server 默认情况下包括的新包，例如 RODBC、[MicrosoftML](../../advanced-analytics/r-services/using-the-microsoftml-package-with-sql-server-r-services.md)、[olapR](../../advanced-analytics/r-services/how-to-create-mdx-queries-using-olapr.md) 和 [sqlrutils](../../advanced-analytics/r-services/how-to-create-a-stored-procedure-using-sqlrutils.md)。
+ 不能再手动更新实例，除非要添加新的包。 

如果你以后决定停止随每个版本升级实例，则必须按[此节](#bkmk_Unbind)中所述**解除绑定**实例，然后按以下文章中所述卸载 Microsoft R Server 组件：[运行 Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)。 该过程完成后，未来的 R Server 升级不会再影响该实例。

> [!NOTE]
> 仅使用累积更新 3.0 修补过的 SQL Server 2016 实例支持该升级过程。  
> 
> 如果在 SQL Server vNext 中使用 R Services，则无需应用此升级。 每个新版本中都会自动升级 R 组件。

## <a name="how-to-upgrade-an-instance"></a>如何升级实例

**先决条件**

1. 标识用于升级的候选实例。 
    + 已安装了 R Services 的 SQL Server 2016
    + Service Pack 1 加 CU3

**获取 R Server**
2. 下载适用于 R Server 9.0.1 的单独 Windows 安装程序
 
    [如何使用独立的 Windows 安装程序在 Windows 上安装 R Server 9.0.1](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#howtoinstall)
3. 在包含要升级的实例的计算机上运行 Microsoft R Server 9.0.1 的新安装程序。

**修改实例以使用 R Server 组件和许可证**
4. 当 Microsoft R Server 安装完成时，找到包含升级实用工具 **SqlBindR.exe** 的文件夹。 

    默认位置是： `C:\Program Files\Microsoft\R Server\Setup`
5. 以管理员身份打开命令提示符并导航到包含 sqlbindr.exe 的文件夹。
6. 键入以下命令，查看可用实例列表： `SqlBindR.exe /list`
   
   记下所列出的完整实例名称。 例如，默认实例可能列出为 `MSSQL13.MSSQLSERVER`。
7. 在使用 */bind* 参数的情况下运行 **SqlBindR.exe** 命令，并指定要升级的实例的名称（如上个步骤中所返回）。 

   例如，若要升级默认实例，请键入： `SqlBindR.exe /bind MSSQL13.MSSQLSERVER`
8. 在升级完成后，重新启动与已修改的任何实例关联的启动板服务。 


## <a name="bkmk_Unbind"></a>如何还原 R Services 的实例

若要还原 SQL Server R Services 的实例以使用原始的 R 库和许可条款，必须运行 SqlBindR 工具来删除绑定，然后修复或重新安装实例。

1. 如上节所述，打开命令提示符并导航到包含 **sqlbindr.exe** 的文件夹。 

2. 在使用 */unbind* 参数的情况下运行 **SqlBindR.exe** 命令，并指定实例。 

   例如，以下命令恢复默认实例，以符合 SQL Server 许可和 SQL Server 更新计划：
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`
2. 通过执行下列操作之一将实例还原到原始状态：
    + 修复实例。 修复操作将更新应用于所有已安装的功能。
    + 卸载并重新安装，然后应用所有的服务版本。 必须重启实例。
3. 删除 R Server 后，还会删除随实例一起安装的任何包，因此必须重新安装。

## <a name="requirements"></a>要求
仅满足以下要求的 SQL Server 2016 的实例支持升级：
+ SQL Server 2016 SP1 或更高版本
+ 已应用累积更新 3.0 (OD)

当前仅支持通过命令行工具进行升级。 

## <a name="sqlbindrexe-command-syntax"></a>sqlbindr.exe 命令语法


### <a name="usage"></a>用法

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parameters

|名称|Description|
|------|------|
|*list*| 显示当前计算机上所有 SQL 数据库实例 ID 的列表|
|*bind*| 将指定的 SQL 数据库实例升级至 R Server 最新版本，并确保实例会自动获取 R Server 的未来升级|
|*unbind*|从指定的 SQL 数据库实例中卸载 R Server 最新版本，并防止未来 R Server 升级影响该实例|

### <a name="errors"></a>错误

该工具返回以下错误消息：

|错误|解决方法|
|------|------|
|绑定实例时出错| 无法绑定实例。 请与支持部门联系获取帮助。|
|实例已绑定| 已运行 *bind* 命令，但指定的实例已绑定。 选择其他实例。|
|实例未绑定| 已运行 *unbind* 命令，但指定的实例未绑定。 选择一个兼容的不同实例。|
|不是有效的 SQL 实例 ID| 键入的实例名称可能不正确。 使用 *list* 参数再次运行该命令，查看可用的实例 ID。|
|未找到任何实例| 此计算机不具有 SQL Server R Services 的实例。|
|实例必须已安装 SQL R Services（数据库内）的兼容版本。| 有关详细信息，请参阅本主题中的兼容性要求。|
|取消绑定实例时出错| 无法取消绑定实例。 请与支持部门联系获取帮助。|
|发生意外错误| 其他错误。 请与支持部门联系获取帮助。  |
|未找到任何 SQL 实例| 此计算机不具有 SQL Server 的实例。 |


## <a name="see-also"></a>另请参阅

[R Server Release Notes](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes)


