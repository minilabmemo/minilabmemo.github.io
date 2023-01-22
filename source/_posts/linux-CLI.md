---
title: "[linux][紀錄]在linux環境下指令操作"
tags:
  - linux
  - CLI
categories:
  - Tech.
  - back-end
  - linux
date: 2020-12-27 10:37:58
---

>紀錄在linux環境下使用command line如何下指令操作 



> 如果曾經維護管理過linux介面環境，或是管理部署，都會需要在命令列介面環境下操作，所以需要了解基礎的指令操作，本篇純記錄用過的linux CLI指令．如果沒有linux環境可以參考另一篇 [[Docker]快速啟動可用VNC進去連線之ubuntu](https://minilabmemo.github.io/2020/09/14/docker-ubuntu-vnc/")，就可以快速練習喔．

＊命令列介面（英語：Command-Line Interface，縮寫：CLI）是在圖形使用者介面得到普及之前使用最為廣泛的使用者介面，它通常不支援滑鼠，使用者通過鍵盤輸入指令，電腦接收到指令後，予以執行。也有人稱之為文字使用者介面（character user interface, CUI）- 維基百科。


### 系統相關資訊
ref:[linux查詢作業系統資訊，CPU物理個數，CPU核心數，邏輯CPU數，記憶體資訊查詢，硬碟資訊查詢](https://www.uj5u.com/caozuo/9727.html)

#### 查詢記憶體大小
```
可以用下述指令:
free  
free -m  //單位
cat /proc/meminfo

aaaa@el1000:~$ free -m
              total        used        free      shared  buff/cache   available
Mem:          31985       17605        3437          71       10941       15137
Swap:             0           0           0
```


#### 查詢CPU資訊
- 查看 CPU 物理個數
aaaa@el1000:~$ grep 'physical id' /proc/cpuinfo | sort -u | wc -l
1
- 查看 CPU 核心數量
aaaa@el1000:~$ grep 'core id' /proc/cpuinfo | sort -u | wc -l
8
- 查看 CPU 執行緒數
aaaa@el1000:~$ cat /proc/cpuinfo| grep "processor"|wc -l
16
aaaa@el1000:~$  grep 'processor' /proc/cpuinfo | sort -u | wc -l
16
- 查看 CPU 型號
aaaa@el1000:~$ cat /proc/cpuinfo | grep name | sort | uniq
model name      : Intel(R) Xeon(R) CPU D-1548 @ 2.00GHz


---------------


#### 基本路徑操作
```
pwd 目前位置
mkdir folder 創建資料夾
mkdir -p folder 如果目錄已存在則不會報錯
mkdir -p Project/a/src  创建多级目录 mkdir -p
touch  檔名.txt 新增空白檔案
ls 列出 -a 含隱藏檔案
cd 進入
cat filename 直接檢視檔案內容
```

#### 檔案文件權限查看
- ls -l 
```
-l 參數可以顯示檔案與目錄的詳細資訊。
-h 參數可以讓輸出的資訊以比較容易閱讀的格式呈現。

```
- -rwxr-xr-x 意思
```
第一位表示文件的類型，-爲文件，d爲目錄
之後每三位代表即用戶、組用戶、其他用戶
其中r表示讀、w表示寫、x表示可執行-表示沒有權限

```
- Linux 系统中采用三位十进制数表示权限，如0755， 0644.
- 一般赋予目录0755权限，文件0644权限。
```
0755
ABCD
A- 0， 表示十进制
B－用户
C－组用户
D－其他用户
 
---  -> 0   (no excute , no write ,no read)
--x  -> 1   excute, (no write, no read)
-w-  -> 2   write 
-wx  -> 3   write, excute
r--  -> 4   read
r-x  -> 5   read, excute
rw-  -> 6   read, write , 
rwx  -> 7   read, write , excute
 
0755->即用户具有读/写/执行权限，组用户和其它用户具有读写权限；
0644->即用户具有读写权限，组用户和其它用户具有只读权限；

```
 Ref: [ls 參數說明](https://blog.gtwang.org/linux/linux-ls-command-tutorial/)


#### vi 文書處理軟體
```
vi test.txt
//輸入i進入編輯模式
//按下ESC回到一般模式
:wq
存檔
:q!
不存檔離開
```

http://linux.vbird.org/linux_basic/0310vi/0310vi.php

#### 刪除
```
rm filename
rm -r dirname/
要刪除目錄, 需要加入 -r 代表 recursive 遞迴刪除, 
使用時要格外小心, 會把目錄內所有檔案及目錄一同刪除．
-f：force=>強制，不會出現警告訊息，會自動忽略不存在的檔案。
$ rm -r dirname/  刪除空目錄,內有檔案或副目錄便不能刪除
各發行版為了安全起見,強制刪除整個根目錄會不能生效，如果真的想刪請見參考用法：
Ref:
https://www.opencli.com/linux/rm-delete-files-directory-command

```




#### 查看檔案大小
```
du "File"
du --block-size=1G "File"  後面不加檔案則是當前目錄
-s, --summarize 只顯示總計
-h, --human-readable 以 K, M, G 為計量單位
du -shc /ftp/*
https://clay-atlas.com/blog/2020/01/11/linux-chinese-tutorial-command-du-check-file-size/
https://blog.xuite.net/cadmus.lin/yo/39567921
```




#### tar 
```
壓縮
tar zcvf FileName.tar.gz
-z  ：透過 gzip  的支援進行壓縮/解壓縮：此時檔名最好為 *.tar.gz
-c  ：建立打包檔案，可搭配 -v 來察看過程中被打包的檔名(filename)
-f filename：-f 後面要立刻接要被處理的檔名

解壓縮
tar zxvf FileName.tar.gz -C /xxx/xxx
-x  ：解打包或解壓縮的功能，可以搭配 -C (大寫) 在特定目錄解開
```





-------
#### wget
wget 是 linux 中除了 curl 外另一個檔案下載的好用工具。
若要下載網路上的檔案，可執行 wget 加上檔案的網址即可立即下載，
```
wget http://xxxx/xxxxx.tar.gz //也支援ftp://協定
-c //檔案續傳，如果下載大型檔案中途斷線，-c 參數從上次中斷的地方繼續下載
-i urls.txt //如果要下載的檔案非常多，可以將網址放進txt裡

more:
https://blog.gtwang.org/linux/linux-wget-command-download-web-pages-and-files-tutorial-examples/
```

#### Ubuntu內建的apt-get指令來完成更新

Update the package list first:
```
sudo apt-get update
```

#### sshpass
- 安裝sshpass
```
apt-get install sshpass
```

-  使用 scp 與 sshpass 即可複製檔案至遠端 SSH 伺服器.
```
$ sshpass -p [使用者密碼] scp -v [本地檔案路徑] [使用者帳號]@[遠端 SSH 伺服器 IP 位址]:[遠端 SSH Server 目錄]
```
Ref:
How to install sshpass on ubuntu?
https://www.codeproject.com/Questions/1179693/How-to-install-sshpass-on-ubuntu
SSH 檔案傳輸
https://artistehsu.pixnet.net/blog/post/257353906


---
更多參考，待讀
[看似比較簡單的Linux推坑教學 Linux CLI 基本教學](https://www.slideshare.net/ssuser6090c0/linux-linux-cli)
