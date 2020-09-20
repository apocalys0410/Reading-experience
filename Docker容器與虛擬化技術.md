# Docker容器與虛擬化技術

Docker 是在 Linux 容器裡運行應用的開發工具，是一種輕量級的虛擬機。
Docker 的設計宗旨為: Build, Ship and Run Any App, Anywhere。
一款產品從開發到測試到上線，從操作系統，到運行環境，再到應用配置，如果環境配置動作麻煩，每換一台機器，就要重來一次，費力費時。

Docker 對開發人員來說，可透過打包容器(打包對象可以是一套應用程式、一套服務、甚至是一個完整的操作系統)，方便的在任何一台主機上或雲端平台上輕鬆的運行。
將應用程式運行在 Docker 容器上，甚至可實現跨平台、跨伺服器的限制，只需要一次配置好環境，換到別的機器上就可以一鍵佈署完成

此種方式意味著簡化了因為各環境不同需要(重新佈署、前置瑣碎的重複調適工作)，大大的提高了工作效率。
EX: 需要將 Server 從地端轉移到 AWS 上，只要使用Docker 容器技術遷移，在新的 Server 上啟動需要的容器即可。

開發人員利用 Docker 可以消除共同協作程式、從本機開發一上到QAT環境時，常常會出現「在我的機器上可正常工作，但上到其他環境怎麼就壞了」的問題。

-----------------------------------------------

## Dockerfile 流程 - 用來構建 Docker 鏡像文件
* 1.編寫Dockerfile文件
* 2.docker build
* 3.docker run<br/>
![GITHUB]( 圖片網址 "圖片名稱")

-----------------------------------------------

## Dockerfile 格式 - 以 Centos 的文件為例

`# 開啟 Dockerfile檔案`<br/>
`mkdir mysql`<br/>
`cd mysql`<br/>
`vim Dockerfile `<br/>

-----------------------------------------------

## Dockerfile 範例 - 以 Mysql 為例

###### # 基礎鏡像 CentOS
`FROM guyton/centos6`

###### # 維護該鏡像的用戶訊息
`MAINTAINER The CentOS Project-MySQL <cloud-ops@centos.org>`

###### # 鏡像操作指令，安裝 MySql
`RUN yum -y update`
`RUN yum -y install mysql mysql-server`

###### # 開啟 MySql 並開權限
`RUN /etc/init.d/mysqld start &&\`
`mysql -e "grant all privileges on *.* to 'root'@'%' indentified by 'test1234';"&&\`
`mysql -e "grant all privileges on *.* to 'root'@'localhost' indentified by 'test1234';"`

###### # 開啟 3306 Port
`EXPOSE 3306`

###### # 啟動容器時要執行的命令
`CMD ["mysqld_safe"]`

-----------------------------------------------

## Dockerfile 說明 - 注意事項

編寫 Dockerfile 時，有嚴格的格式需要遵循:

- [x] 最初 - 需使用 FROM 指名所基於的鏡像名稱
- [x] 接著 - 需使用 MAINTAINER 說明維護該鏡像的用戶信息
- [x] 接著 - 鏡像操作相關的指令(如 RUN 來運行每一條指令)
- [x] 最後 - 使用 CMD 來指定啟動後容器要運行的命令操作

-----------------------------------------------



