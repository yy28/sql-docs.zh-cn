---
title: "步骤 1： 配置用于 Ruby 开发的开发环境 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8cdbadeb-f640-406c-977c-d2d44b7b5368
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d722d1eed21162d5e076f5dfdfc3a2f18787f42e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>步骤 1： 配置用于 Ruby 开发的开发环境
你将需要配置你的开发环境满足先决条件才能开发应用程序使用的 SQL Server Ruby 驱动程序。    
  
请注意，Ruby 驱动程序使用 TDS 协议，默认情况下，SQL Server 和 Azure SQL 数据库中启用。  这种方式无需任何其他配置。  
  
  
## <a name="windows"></a>Windows  
  
1.  **下载 Ruby 安装程序**  
如果您的计算机没有 Ruby，请安装它。 对于新的 ruby 用户，我们建议使用 Ruby 2.2.X 安装程序。 这些提供稳定语言和扩展的包 (gem) 兼容且更新列表。 请转到[Ruby 下载页](http://rubyinstaller.org/downloads/)并下载适当的 2.1.x 安装程序。 例如，如果您是在 64 位计算机上，下载 Ruby 2.1.6 (x64) 安装程序。   
  
2.  **安装 Ruby**  
安装程序在下载之后，执行以下操作：  
a. 双击文件以启动安装程序。  
b. 选择你的语言，并同意这些条款。  
c.  在安装设置屏幕中，选择对路径和将.rb 和.rbw 文件与此 Ruby 安装这两个添加 Ruby 可执行文件旁边的复选框。  
  
3.  **下载 Ruby DevKit**  
从 RubyInstaller 页下载 DevKit  
  
4.  **安装 Ruby DevKit**  
下载完成后，请执行以下操作：  
a. 双击该文件。 将会要求你提取文件的位置。  
b. 单击"..."按钮，然后选择"C:\DevKit"。 你可能需要首先创建此文件夹，通过单击"新建文件夹"。  
c. 单击"确定"，和然后"提取"，提取文件。  
  
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
  
2. **安装 Ruby 版本管理器 (rvm) 和先决条件**  
```  
> sudo apt-get --assume-yes update  
> command curl -sSL https://rvm.io/mpapis.asc | gpg --import -  
> curl -L https://get.rvm.io | bash -s stable  
> source ~/.rvm/scripts/rvm  
```  
   
3. **使用 rvm 安装 Ruby**  
例如，安装 Ruby 的版本 2.3.0:  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;确保最后一个命令的输出将指示你运行的版本 2.3.0。  
  
4.  **安装 FreeTDS**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **安装 TinyTDS**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
请注意，Mac OS X 已有 Ruby 预安装，如操作系统具有依赖关系。    
  
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
