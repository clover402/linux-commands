## 安装package controll
### 自动安装
control+`打开控制台输入下面命令
```
import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```
回车后即可自动安装完成

### 手动安装
1. Click the Preferences > Browse Packages… menu
2. Browse up a folder and then into the Installed Packages/ folder
3. Download [Package Control.sublime-package](https://packagecontrol.io/Package%20Control.sublime-package) and copy it into the Installed Packages/ directory
4. Restart Sublime Text

参考：https://packagecontrol.io/installation#st3


## 安装插件SublimeREPL
1. install sublimeREPL
2. 设置快捷键.首选项->按键绑定-用户,填写如下内容
```
{
    "keys": ["ctrl+f5"],
    "caption": "SublimeREPL: Python - RUN current file",
    "command": "run_existing_window_command",
    "args": {
        "id": "repl_python_run",
        "file": "config/Python/Main.sublime-menu"
    }
}
```
3. 如此之后可直接在编辑器界面按快捷键执行python脚本


## 常用插件
1. Alignment  自动对齐
2. Bracket Highlighter  高亮显示括号、引号、标签
3. SublimeLinter 高亮显示不规范的错误的写法
4. PackageResourceViewer 插件源码查看器

## 安装phpcs
1. sublime安装phpcs插件,ctrl+shift+p->install->phpcs
2. [下载phpcs-fixer](http://cs.sensiolabs.org/),把php-cs-fixer.phar 放到你的 php.exe 安装目录
3. [下载php CodeSniffer](http://download.pear.php.net/package/PHP_CodeSniffer-1.5.0RC4.tgz/)
4. 修改sublime phpcs配置文件，设置如下
```
// This is needed as we cannot run phars on windows, so we run it through php
"phpcs_php_prefix_path": "D:\\path\\to\\php\\php.exe",

// This is the path to the bat file when we installed PHP_CodeSniffer
"phpcs_executable_path": "D:\\path\\to\\phpCodeSniffer\\phpcs.bat",

// The fixer phar file is stored here:
"php_cs_fixer_executable_path": "D:\\path\\to\\phpcs-fixer\\php-cs-fixer.phar",

// Path to php
"phpcs_php_path": "D:\\path\\to\\php\\php.exe",
```
5. 如出现"UnicodeDecodeError: 'utf-8' codec can't decode..."错误，可以用packageResourceViewer打开phpcs.py,修改183行return data.decode()
为return data.decode('gbk')
6. 如还无法使用可以在phpcs.py中打印data.decode('gbk')查看具体错误。我出现了@php_bin@不是内部变量的错误，追踪代码发现是phpcs.bat写得有问题，修改所有的环境变量**@php_bin@**,**@php_dir@**,**@bin_dir@**为真实内容即可

## 安装配置ctags插件
1. 下载ctags程序，[下载地址](http://prdownloads.sourceforge.net/ctags/ctags58.zip)
2. 安装ctags插件
3. 配置路径，首选项-》插件管理-》ctags  复制default的配置内容到user，修改commands后面的路径为ctags.exe的完整路径（路径最好不含中文）
4. 配置快捷键，首选项-》插件管理-》ctags 复制default的内容到user，修改为你喜欢的快捷键


## 新建php编译系统
1. 工具-》编译系统-》新建编译系统
2. 输入如下内容保存
```
{
    "cmd": ["php", "$file"],
    "file_regex": "^(...*?):([0-9]*):?([0-9]*)",
    "selector": "source.php"
}
```
默认保存路径：D:\Sublime Text3\Data\Packages\User\php.sublime-build

3. php文件可以直接ctrl+b直接运行

## xdeubg[WINDOWS]
### 安装xdubug
1. 显示phpinfo的内容，查看源码，复制放到如下地址 https://xdebug.org/wizard.php ,会自动显示对于的xdebug版本
2. 下载xdebug，放入php的ext文件夹
3. 修改php.ini配置文件，加入如下内容
```
zend_extension = ext\php_xdebug-2.5.4-7.1-vc14-x86_64.dll
[xdebug]
xdebug.remote_enable=1
xdebug.remote_handler=dbgp
xdebug.remote_host=127.0.0.1
xdebug.remote_port=9999 
```
注意：xdebug端口号要与php-cgi的不同

4. 重启php-cgi与 nginx
### chrome浏览器安装插件
1. 下载xdebug-helper插件并安装
2. 安装完后设置ide-key：sublime.xdebug
### sublime安装xdebug client
1. ctrl+alt+p -> install -> xdebug client
2. 首选项 -> 插件设置 -> xdebug -> 复制default内容到user
3. 编辑如下几行
```
"url":"http://localhost/", #调试的地址
"port":9999,
"ide_key": "sublime.xdebug",
```
注意：端口号与php.ini中xdebug设置一致

4. 快捷键
* ctrl+shift+F9 开始调试
* ctrl+F8 断点设置
* ctrl+shift+F10 结束调试
* ctrl+shift+F5 到下一个断点
* Ctrl+Shift+F6: 单步
* Ctrl+Shift+F7: 步入
* Ctrl+Shift+F8: 步出

### curl命令调试
1. windows环境需要安装curl命令
2. 对于api调试可以在chrome浏览器中打开开发者工具，查看网络，选中右键，copy，copy as curl（bash），如果cookie中没有XDEBUG_SESSION=sublime.xdebug，还需要补充上。sublime中crtl+shift+F9开启xdebug调试，在命令行中运行即可开始调试
3. 也可以直接用curl命令进行调试
```
curl -b XDEBUG_SESSION=sublime.xdebug -X POST -d 'a1=xxx&a2=xxx' -m 300 url_to_debug
```
