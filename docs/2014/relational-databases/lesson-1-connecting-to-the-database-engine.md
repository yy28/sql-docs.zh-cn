---
title: 第 1 课：连接到数据库引擎 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e8db82f0-50ed-4531-9209-940006ed34cb
author: rothja
ms.author: jroth
ms.openlocfilehash: d296aae78434bcfff1c69770878705ef5f4bd0ae
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025350"
---
# <a name="lesson-1-connecting-to-the-database-engine"></a>第 1 课：连接到数据库引擎
  安装 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]时，安装哪些工具取决于版本和您的安装选择。 本课将介绍主要的工具以及如何连接并执行一项基本功能（授权多个用户）。  
  
  
  
##  <a name="tools-for-getting-started"></a><a name="tools"></a>用于入门的工具  
 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 提供了多种工具。 本主题说明您首先需要的工具，并帮助选择适合于作业工具。 所有工具都可以从“开始”**** 菜单上访问。 默认情况下不会安装 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 之类的一些工具。 必须在安装过程中将这些工具选择为客户端组件的一部分。 有关下面所述工具的完整说明，请在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机图书中进行搜索。 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 仅包含其中的一部分工具。  
  
### <a name="basic-tools"></a>基本工具  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 是管理[!INCLUDE[ssDE](../includes/ssde-md.md)]和编写 [!INCLUDE[tsql](../includes/tsql-md.md)] 代码的主要工具。 它驻留在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 外壳中。 它未包含在中， [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 但可从[Microsoft 下载中心](https://go.microsoft.com/fwlink/?LinkId=144346)单独下载。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 配置管理器同 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和客户端工具一起安装。 使用它，您可以启用服务器协议，配置协议选项（例如 TCP 端口），将服务器服务配置为自动启动，以及将客户端计算机配置为以所需的方式连接。 此工具会配置更高级的连接元素，但不会启用功能。  
  
### <a name="sample-database"></a>示例数据库  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]不包含示例数据库和示例。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 联机丛书中所述的大多数示例都使用 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 示例数据库。  
  
##### <a name="to-start-sql-server-management-studio"></a>启动 SQL Server Management Studio  
  
-   在 "**开始**" 菜单上，指向 "**所有程序**"，指向 [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] ""，然后单击 " **SQL Server Management Studio**"。  
  
##### <a name="to-start-sql-server-configuration-manager"></a>启动 SQL Server 配置管理器  
  
-   在 **“开始”** 菜单中，依次指向 **“所有程序”** 、 [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]、 **“配置工具”** ，然后单击 **“SQL Server 配置管理器”** 。  
  
##  <a name="connecting-with-management-studio"></a><a name="connect"></a>连接 Management Studio  
 如果知道实例名并且以计算机上的 Administrators 组成员身份进行连接，则可以使用同一台计算机上运行的工具轻松连接到[!INCLUDE[ssDE](../includes/ssde-md.md)]。 必须在承载 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的同一台计算机上执行下面的过程。  
  
##### <a name="to-determine-the-name-of-the-instance-of-the-database-engine"></a>确定数据库引擎实例的名称  
  
1.  以 Administrators 组成员身份登录到 Windows，然后打开 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。  
  
    > [!IMPORTANT]  
    >  如果要连接到 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)] 或 [!INCLUDE[nextref_longhorn](../includes/nextref-longhorn-md.md)] （或更高），则可能需要右键单击 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] ，然后单击 "以**管理员身份运行**" 以便使用您的管理员凭据进行连接。 从 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 开始，安装程序将所选登录名添加到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，这样就不再需要管理员凭据了。  
  
2.  在 **“连接到服务器”** 对话框中，单击 **“取消”**。  
  
3.  如果未显示“已注册的服务器”，请在“视图”**** 菜单中，单击“已注册的服务器”****。  
  
4.  在“已注册的服务器”工具栏中选择“数据库引擎”**** 后，展开“数据库引擎”****，右键单击“本地服务器组”****，指向“任务”****，然后单击“注册本地服务器”****。 将显示计算机上安装的所有[!INCLUDE[ssDE](../includes/ssde-md.md)]实例。 默认实例未命名，并显示为计算机名称。 命名实例显示为计算机名称，后跟反斜杠 (\\)，然后是实例名。 对于 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]，除非在安装过程中更改了名称，否则实例将命名为 *<computer_name>* \sqlexpress。  
  
##### <a name="to-verify-that-the-database-engine-is-running"></a>验证数据库引擎是否正在运行  
  
1.  在“已注册的服务器”中，如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的名称中有绿色的点并在名称旁边有白色箭头，则表示 [!INCLUDE[ssDE](../includes/ssde-md.md)] 正在运行，无需执行其他操作。  
  
2.  如果 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例的名称中有红色的点并在名称旁边有白色正方形，则表示[!INCLUDE[ssDE](../includes/ssde-md.md)]已停止。 右键单击 [!INCLUDE[ssDE](../includes/ssde-md.md)] 的名称，单击“服务控制”****，然后单击“开始”****。 出现确认对话框之后，[!INCLUDE[ssDE](../includes/ssde-md.md)]应启动，圆圈应变为绿色且带有白色箭头。  
  
##### <a name="to-connect-to-the-database-engine"></a>连接到数据库引擎  
  
1.  在 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 中的“文件”**** 菜单上，单击“连接对象资源管理器”****。  
  
     将打开“连接到服务器”**** 对话框。 “服务器类型”**** 框中将显示上次使用的组件的类型。  
  
2.  选择“数据库引擎”。  
  
3.  在“服务器名称”**** 框中，键入 [!INCLUDE[ssDE](../includes/ssde-md.md)] 实例的名称。 对于默认的 SQL Server 实例，服务器名称即计算机名称。 对于 SQL Server 的命名实例，服务器名称是 *<computer_name>***\\***<* instance_name **> ACCTG_SRVR。**  
  
4.  单击“连接”。  
  
##  <a name="authorizing-additional-connections"></a><a name="additional"></a>授权其他连接  
 现在，您已经以管理员身份连接到了 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ，您的首要任务之一是授权其他用户进行连接。 实现此任务的步骤是创建一个登录名，然后授权此登录名以用户身份访问数据库。 登录名可以是使用 Windows 凭据的 Windows 身份验证登录名；也可以是 SQL Server 身份验证登录名（这些登录名在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中存储身份验证信息并独立于 Windows 凭据）。 尽可能使用 Windows 身份验证。  
  
##### <a name="create-a-windows-authentication-login"></a>创建 Windows 身份验证登录名  
  
1.  在上一个任务中，您使用 [!INCLUDE[ssDE](../includes/ssde-md.md)] 连接到了[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]。 在对象资源管理器中，依次展开服务器实例、“安全性”****，右键单击“登录名”****，再单击“新建登录名”****。  
  
     将显示“登录名 - 新建”**** 对话框。  
  
2.  在 "**常规**" 页上的 "**登录名**" 框中，以* \<domain> \\<Login \> *格式键入 Windows 登录名。  
  
3.  在“默认数据库”**** 框中，选择 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]（如果有）。 否则选择“master”****。  
  
4.  在“服务器角色”**** 页中，如果新建登录名要成为管理员，则单击“sysadmin”****，否则保留此项为空白。  
  
5.  在“用户映射”**** 页中，针对 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 数据库（如果有）选择“映射”****。 否则选择“master”****。 注意，“用户”**** 框使用该登录名进行填充。 关闭后，该对话框将在数据库中创建此用户。  
  
6.  在“默认架构”**** 框中，键入 **dbo** 将登录名映射到数据库所有者架构。  
  
7.  接受“安全对象”**** 和“状态”**** 框的默认设置，然后单击“确定”**** 创建登录名。  
  
> [!IMPORTANT]  
>  这是基本的入门信息。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 提供了丰富的安全环境，而安全显然是数据库操作的一个重要方面。  
  
## <a name="next-lesson"></a>下一课  
 [第 2 课：从其他计算机进行连接](lesson-2-connecting-from-another-computer.md)  
  
  
