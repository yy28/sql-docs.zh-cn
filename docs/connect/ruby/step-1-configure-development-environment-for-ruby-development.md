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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 38af92d3cb0354bc4b75131a349f6a1c26e90490
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992459"
---
# <a name="step-1-configure-development-environment-for-ruby-development"></a>步骤 1：配置用于 Ruby 开发的开发环境
你将需要使用系统必备组件来配置开发环境, 以便使用 SQL Server 的 Ruby 驱动程序开发应用程序。    
  
请注意, Ruby 驱动程序使用 TDS 协议, 该协议默认情况下在 SQL Server 和 Azure SQL 数据库中启用。  这种方式无需任何其他配置。  
  
  
## <a name="windows"></a>Windows  
  
1.  **下载 Ruby 安装程序**  
如果您的计算机没有 Ruby, 请安装它。 对于新的 ruby 用户, 建议使用 Ruby 2.2. X 安装程序。 它们提供了一种稳定的语言, 以及兼容和更新的包 (gem) 的广泛列表。 请在[Ruby 下载页](https://rubyinstaller.org/downloads/)上, 下载相应的 2.1. x 安装程序。 例如, 如果你使用的是64位计算机, 请下载 Ruby 2.1.6 (x64) 安装程序。   
  
2.  **安装 Ruby**  
下载安装程序后, 请执行以下操作:  
A. 双击该文件以启动安装程序。  
B. 选择语言, 并同意条款。  
c.  在 "安装设置" 屏幕上, 选中 "将 Ruby 可执行文件添加到路径" 旁边的复选框, 并将 rbw 文件与此 Ruby 安装相关联。  
  
3.  **下载 Ruby DevKit**  
从 RubyInstaller 页面下载 DevKit  
  
4.  **安装 Ruby DevKit**  
下载完成后, 请执行以下操作:  
A. 双击该文件。 系统会询问你要将文件提取到何处。  
B. 单击 "..."按钮, 然后选择 "C:\DevKit"。 您可能需要首先单击 "新建文件夹" 来创建此文件夹。  
c. 单击 "确定", 然后单击 "提取" 以提取文件。  
  
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
例如, 安装 Ruby 的版本 2.3.0:  
```  
> rvm install 2.3.0  
> rvm use 2.3.0 --default  
> ruby -v  
```  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;确保最后一个命令的输出指示你正在运行版本2.3.0。  
  
4.  **安装 FreeTDS**  
```  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
```  
  
5.  **安装 TinyTDS**  
```  
> gem install tiny_tds  
```  
  
## <a name="mac"></a>Mac  
  
请注意, Mac OS X 已预先安装了 Ruby, 因为操作系统具有依赖关系。    
  
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
