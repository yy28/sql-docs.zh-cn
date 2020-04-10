---
title: 步骤 1：配置用于 Ruby 开发的开发环境 | Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ce61e3fb360d4c8a4db8f717f10b7d107245300
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926738"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>步骤 1：配置用于 Ruby 开发的开发环境
必须为开发环境配置必备项，才能使用 Ruby Driver for SQL Server 开发应用程序。    
  
请注意，Ruby 驱动程序使用 TDS 协议，SQL Server 和 Azure SQL 数据库中默认启用此协议。  这种方式无需任何其他配置。  
  
  
## <a name="windows"></a>Windows  
  
1.  **下载 Ruby 安装程序**  
如果计算机上没有 Ruby，请安装它。 对于刚开始接触 Ruby 的用户，建议使用 Ruby 2.2.X 安装程序。 这些安装程序提供稳定的语言，以及一个包含大量兼容且已更新的包 (gem) 的列表。 转到 [Ruby 下载页](https://rubyinstaller.org/downloads/)，并下载相应 2.1.x 安装程序。 例如，如果你使用 64 位计算机，请下载 Ruby 2.1.6 (x64) 安装程序。   
  
2.  **安装 Ruby**  
下载安装程序后，请执行以下操作：  
a. 双击文件，以启动安装程序。  
b.保留“数据库类型”设置，即设置为“共享”。 选择语言，并同意接受条款。  
c.  在“安装设置”屏幕上，选中“将 Ruby 可执行文件添加到 PATH”和“将 .rb 和 .rbw 文件与此 Ruby 安装相关联”旁边的复选框。  
  
3.  **下载 Ruby DevKit**  
从 RubyInstaller 页下载 DevKit  
  
4.  **安装 Ruby DevKit**  
下载完成后，请执行以下操作：  
a. 双击文件。 系统会询问要从哪里提取文件。  
b.保留“数据库类型”设置，即设置为“共享”。 单击“...”按钮，然后选择“C:\DevKit”。 可能需要先单击“新建文件夹”来创建此文件夹。  
c. 依次单击“确定”和“提取”，以提取文件。  
  
5. **打开 cmd.exe**  
  
6. **初始化 Ruby DevKit**  
```  
> chdir C:\DevKit  
> ruby dk.rb init  
> ruby dk.rb install  
```  
  
7.  **安装 TinyTDS gem**  
```  
> gem inst tiny_tds
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **打开终端**  
  
2. **安装 Ruby 版本管理器 (rvm) 和系统必备**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **使用 rvm 安装 Ruby**  
例如，安装 Ruby 版本 2.3.0：  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;请确保最后一个命令的输出指明运行的版本是 2.3.0。  
  
4.  **安装 FreeTDS**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **安装 TinyTDS**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
请注意，Mac OS X 已预安装 Ruby，因为 OS 有依赖项。    
  
1.  **打开终端**  
  
2. **安装 Homebrew 包管理器**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
3.  **安装 FreeTDS**  
```  
> brew install FreeTDS  
```  
  
4.  **安装 TinyTDS gem**  
```  
> gem install tiny_tds  
```
