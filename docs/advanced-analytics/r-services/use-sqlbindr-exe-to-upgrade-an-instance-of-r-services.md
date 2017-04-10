---
title: "使用 sqlBindR.exe 升级 R Services 的实例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server (starting with 2016 CTP3)"
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# 使用 sqlBindR.exe 升级 R Services 的实例
Microsoft R Server for Windows 包含名为 **SqlBindR.exe** 的新工具，可用于升级实例的 R 组件。 此过程称为**绑定**，因为它会更改 SQL Server 2016 实例的许可模式，使用新的 Microsoft 新式软件生命周期支持许可证。

一般情况下，此许可系统可确保数据科学家始终使用 R 的最新版本。若要深入了解 Microsoft 软件许可证的条款和优点，请参阅[运行 Microsoft R Server for Windows](https://msdnstage.redmond.corp.microsoft.com/en-us/microsoft-r/rserver-install-windows?branch=r-server-nov16-dev)。

绑定实例时，将出现三种情况：
+ 实例的支持策略由 SQL Server 2016 支持策略更改为新的 Microsoft 新式软件许可协议。
+ 通过 R Server 版本（当前位于新的新式软件许可条款下）中的锁定步骤，与该实例关联的 R 组件将随每个版本自动升级。
+ 不能再手动更新实例，除非要添加新的包。 

如果以后决定停止升级每个版本中的实例，必须**解除绑定**该实例，然后卸载 Microsoft R Server 组件，如[运行 Microsoft R Server for Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows) 一文所述。 该过程完成后，未来的 R Server 升级不会再影响该实例。

> [!NOTE] 仅使用累积更新 3.0 修补过的 SQL Server 2016 实例支持该升级过程。  
> 
> 如果在 SQL Server vNext 中使用 R Services，则无需应用此升级。 每个新版本中都会自动升级 R 组件。

## <a name="how-to-upgrade-an-instance"></a>如何升级实例


1. 在包含要升级的实例的计算机上运行 Microsoft R Server 安装程序。
2. 安装完成后，找到包含工具 **SqlBindR.exe** 的文件夹。 默认位置是：`C:\Program Files\Microsoft\R Server\Setup`
2. 以管理员身份打开命令提示符。
3. 键入以下命令，查看可用实例列表：`SqlBindR.exe /list`
4. 运行具有 */bind* 参数的 **SqlBindR.exe** 命令，指定要升级的实例的名称。 
   例如，若仅升级默认实例，请键入： `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

## <a name="how-to-downgrade-an-instance-of-r-services"></a>如何降级 R Services 的实例

若要恢复实例的状态，必须运行 SqlBindR 工具删除许可，然后修复或重新安装该实例。

1. 运行具有 */unbind* 参数的 **SqlBindR.exe** 命令，并指定实例。 
   例如，以下命令恢复默认实例，以符合 SQL Server 许可和 SQL Server 更新计划： `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`
2. 通过执行下列操作之一将实例还原到原始状态：
    + 修复实例。 修复操作将更新应用于所有已安装的功能。
    + 卸载并重新安装，然后应用所有的服务版本。 必须重启实例。
3. 删除 R Server 后，也会删除随实例一起安装的任何包，因此必须重新安装。

## <a name="requirements"></a>要求
仅满足以下要求的 SQL Server 2016 的实例支持升级：
+ SQL Server 2016 SP1 或更高版本
+ 已应用累积更新 3.0 (OD)

当前仅支持通过命令行工具进行升级。 更高版本将提供交互式界面。

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
|实例未绑定| 已运行 *unbind* 命令，但指定的实例未绑定。 选择其他实例。|
|不是有效的 SQL 实例 ID| 键入的实例名称可能不正确。 使用 *list* 参数再次运行该命令，查看可用的实例 ID。|
|未找到任何实例| 此计算机不具有 SQL Server R Services 的实例。|
|实例必须已安装 SQL R Services（数据库内）的兼容版本。| 有关详细信息，请参阅 https://go.microsoft.com/fwlink/?linkid=835761|
|取消绑定实例时出错| 无法取消绑定实例。 请与支持部门联系获取帮助。|
|发生意外错误| 其他错误。 请与支持部门联系获取帮助。  |
|未找到任何 SQL 实例| 此计算机不具有 SQL Server 的实例。 |


## <a name="see-also"></a>另请参阅

[R Server Release Notes](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes)（R Server 发行说明）
