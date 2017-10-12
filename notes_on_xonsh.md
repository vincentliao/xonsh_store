# Notes on Xonsh, Xon.sh

## 安裝 Xonsh

由於 xonsh 得透過 `Python 3.4+` 來執行，因此相關的套件安裝，有時候真的得弄清楚一點: 
```
$ pip3 install xonsh
```

## 設定帳號使用的 shell 

編輯 `/etc/shells` 檔案，在尾端新增一行 `/usr/local/bin/xonsh`，然後透過下面指令修改

```
$ chsh -s /usr/local/bin/xonsh 
```

## 指令無法使用 ? 

這恐怕是 Unix 的老問題，就是執行路徑的問題，所以先檢查環境變數 `$PATH` 是不是符合預期 ? 比方說安裝 `xonsh` 後，Home Brew 就不能用了，原來是 `$PATH` 沒有 `/usr/local/bin`，請用下面的指令新增: 

```python
$ print($PATH)
['/usr/bin', '/bin', '/usr/sbin', '/sbin']

$ $PATH.append('/usr/local/bin')
```

當然要一勞永逸，就應該去修改設定檔 `~/.xonshrc` 檔案，加上這行:

```python
$PATH = ['/usr/bin', '/bin', '/usr/sbin', '/sbin', '/usr/local/bin']
```

## 如果想要有 `fish` shell 的 auto-complete

在[這裡](https://github.com/xonsh/xonsh/issues/272)有人建議作者 [Anthony](https://github.com/scopatz) 幫忙加上這個很不錯的功能。

```
$ xonsh --shell-type='prompt_toolkit'
```
或是在 `~/.xonsh` 中指定 shell type: 

```
$SHELL_TYPE = 'prompt_toolkit'
```

安裝套件也要記得弄清楚 `Python` 版本，不然就算安裝了，也取用不到。像是 shell type 中要用到 `prompt_toolkit` 這個套件，所以如果你用 `pip` 安裝了 `prompt_toolkit`，依然會出錯: 

```shell
$ xonsh --shell-type='prompt_toolkit'

/usr/local/Cellar/xonsh/0.5.12/libexec/lib/python3.6/site-packages/xonsh/__amalgam__.py:14195: UserWarning: prompt_toolkit is not available, using readline instead.
  warnings.warn('prompt_toolkit is not available, using '
```

看了錯誤訊息，知道 `xonsh` 的程式碼從 `python3.6` 的目錄下取用不到 `prompt_toolkit` 模組，所以你得替 `Python 3.6` 安裝好 `prompt_toolkit`：

```
$ pip3.6 install prompt_toolkit
```

## 如果在互動模式中，想要有即時的顏色

最初用 HomeBrew 安裝 `xonsh` 結果套件亂成一團，顏色都出不來，看了 2016 年 pycon 的中 Anthony 的影片，似乎用 `pip` 安裝，於是全部都移除後，改用 `pip3.6` 安裝，也誤打誤撞重新安裝了 `Pygments`  套件後，顏色就出來了。


