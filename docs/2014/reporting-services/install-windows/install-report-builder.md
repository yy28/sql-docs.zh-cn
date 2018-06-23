---
title: 安装报表生成器 （报表生成器） 的独立版本 |Microsoft 文档
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
caps.latest.revision: 10
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 599f5aef18b38070d1543de351d0f99b68b4596e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127661"
---
# <a name="install-the-stand-alone-version-of-report-builder-report-builder"></a>安装报表生成器的独立版本（报表生成器）
  你可以安装从报表生成器[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]上功能包[Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=168472)或如 ReportBuilder3_x86.msi，报表生成器中，Windows Installer 包具有的公用文件夹的位置已下载。  
  
 还可以执行报表生成器的命令行安装，并提供参数以自定义安装。 除了标准的 MSI 内部参数以外，还可以使用报表生成器提供的自定义参数：RBINSTALLDIR 和 REPORTSERVERURL。 RBINSTALLDIR 指定报表生成器的根安装文件夹。 REPORTSERVERURL 指定报表生成器用于在服务器上保存报表的默认报表服务器。  
  
 如果要进行根本没有用户界面交互的完全静默安装，请指定 **/quiet** 选项。 根据设计，quiet 选项标志会隐藏安装错误。 因此，建议在使用 quiet 选项时包括 **/l** 选项，该选项指定进行日志记录。  
  
> [!IMPORTANT]  
>  Windows Vista 和 Windows 7 安全功能需要提升权限以运行命令行操作，并将提示您提供运行命令行的权限。 安装不是静默的。 若要进行静默安装，您需要以管理员身份运行命令行。  
  
### <a name="to-install-report-builder-from-the-download-site"></a>从下载站点安装报表生成器  
  
1.  转到[Microsoft SQL Server 2012 报表生成器](http://go.microsoft.com/fwlink/?LinkID=219138)找到 Web 页的报表生成器部分。  
  
2.  单击**X86 包**。  
  
3.  在**文件下载**对话框中，单击**运行**。  
  
    > [!IMPORTANT]  
    >  请仅下载来自可信来源的文件。  
  
4.  在 Internet 资源管理器对话框中，单击**运行**。  
  
    > [!IMPORTANT]  
    >  请仅运行来自可信来源的文件。  
  
5.  Microsoft SQL Server 报表生成器向导将会启动。  
  
6.  上**欢迎使用安装向导**页上，单击**下一步**。  
  
7.  上**许可协议**页上，阅读协议，然后选择**我接受许可协议中的条款**选项。 单击“下一步” 。  
  
8.  提供个人姓名和公司名称。 单击“下一步” 。  
  
9. 上**功能选择**页上，（可选） 单击**浏览**或**磁盘成本**。 单击“下一步” 。  
  
    -   单击**浏览**若要查看的报表生成器的默认位置，并更新它。  
  
        > [!NOTE]  
        >  报表生成器的默认安装文件夹是\<驱动器 > Program Files\Microsoft SQL Server。  
  
    -   单击**磁盘成本**若要了解报表生成器多少磁盘空间使用。  
  
        > [!NOTE]  
        >  如果某个卷没有足够数量的可用磁盘空间，则该卷会突出显示。  
  
10. 在 **“默认的目标服务器”** 页上，如果目标报表服务器的 URL 与默认 URL 不同，则可选择提供前者。 单击“下一步” 。  
  
    > [!NOTE]  
    >  如果计划在报表生成器连接到某个报表服务器时使用它，则此时提供该报表服务器的 URL 将会非常方便。 但是，你也可以这样做从**选项**对话框中，当您在报表生成器中工作。  
  
11. 单击**安装**以完成安装报表生成器。  
  
### <a name="to-install-report-builder-from-a-share"></a>从共享位置安装报表生成器  
  
1.  请与管理员联系，以获得在本地计算机上安装报表生成器所要运行的 ReportBuilder3_x86.msi.msi 的位置。  
  
2.  浏览找到 ReportBuilder3_x86.msi.msi（报表生成器的 Windows Installer 包 (MSI)），然后单击它。  
  
     Microsoft SQL Server 报表生成器向导将会启动。  
  
3.  上**欢迎使用安装向导**页上，单击**下一步**。  
  
4.  上**许可协议**页上，阅读协议，然后选择**我接受许可协议中的条款**选项。 单击“下一步” 。  
  
5.  提供个人姓名和公司名称。 单击“下一步” 。  
  
6.  上**功能选择**页上，（可选） 单击**浏览**或**磁盘成本**。 单击“下一步” 。  
  
    -   单击**浏览**若要查看的报表生成器的默认位置，并更新它。  
  
        > [!NOTE]  
        >  报表生成器的默认安装文件夹是\<驱动器 > Program Files\Microsoft SQL Server。  
  
    -   单击**磁盘成本**若要了解报表生成器多少磁盘空间使用。  
  
        > [!NOTE]  
        >  如果某个卷没有足够数量的可用磁盘空间，则该卷会突出显示。  
  
7.  在 **“默认的目标服务器”** 页上，如果目标报表服务器的 URL 与默认 URL 不同，则可选择提供前者。 单击“下一步” 。  
  
    > [!NOTE]  
    >  如果计划在报表生成器连接到某个报表服务器时使用它，则此时提供该报表服务器的 URL 将会非常方便。 但是，你也可以这样做从**选项**对话框中，当您在报表生成器中工作。  
  
8.  单击**安装**以完成安装报表生成器。  
  
### <a name="to-install-report-builder-from-the-command-line"></a>从命令行安装报表生成器  
  
1.  转到[Microsoft SQL Server 2012 报表生成器](http://go.microsoft.com/fwlink/?LinkID=219138)找到的报表生成器部分。  
  
2.  单击**X86 包**。  
  
3.  单击“保存”。  
  
4.  （可选） 浏览到要保存到、 验证位置**将另存为**选项**Windows Installer 包**，然后单击**保存**。  
  
5.  在 **“开始”** 菜单上，单击 **“运行”**。  
  
6.  在打开的文本框中，键入 `cmd.`  
  
7.  在命令提示符窗口中，导航到要保存 ReportBuilder3_x86.msi 的文件夹。  
  
8.  使用以下格式键入命令：  
  
     `msiexec/i ReportBuilder3_.msi /option [value] [/option [value]]`  
  
     安装报表生成器的两个特定选项为：RBINSTALLDIR 和 REPORTSERVERURL。 不需要在命令行中包含这些参数。 以下为基准命令：  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
9. 若要运行命令，请按 Enter。  
  
## <a name="see-also"></a>请参阅  
 [安装、 卸载和报表生成器支持](../install-uninstall-and-report-builder-support.md)   
 [卸载报表生成器的独立版本&#40;报表生成器&#41;](install-report-builder.md)  
  
  