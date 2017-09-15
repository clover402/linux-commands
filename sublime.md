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
3. phpcs 支持php语法
4. SublimeLinter 高亮显示不规范的错误的写法

## 安装配置ctags插件
1. 下载ctags程序，[http://prdownloads.sourceforge.net/ctags/ctags58.zip](下载地址)
2. 安装ctags插件
3. 配置路径，首选项-》插件管理-》ctags  复制default的配置内容到user，修改commands后面的路径为ctags.exe的完整路径（路径最好不含中文）
4. 配置快捷键，首选项-》插件管理-》ctags 复制default的内容到user，修改为你喜欢的快捷键
