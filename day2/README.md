# Docker practice DAY2

 `winpty docker pull centos`
 * winpty : 提供該指令所需的tty，防止亂碼
 * docker pull &lt;images> : 下載要的映像檔

`docker images`
* 列出已有的映像檔
 >* repository : 來自哪個倉庫
 * tag : 區分同倉庫中不同的映像檔(沒有的話預設是latest)
 * image id : 唯一的，若這個相同表示是同一個映像檔
 * created : 建立時間
 * virtual size : 他的大小

`winpty docker run -t -i centos bash`
 * -i 讓標準輸入維持在打開的狀態
 * -t 替容器配置一個虛擬的終端機
 * bash : shell工具的運行地址
 *(/bin/bash ERROR occured --> Solution : bash)*


## 進入該容器後
 *表示的樣子 : `root@\<containerID>:/#`*

`gem install json`
* 加入json的gem套件
 * problem : gem版本過舊
 * solution : 升級ruby
 `rvm install ruby 2.6.3`

	#安裝RVM(管理ruby/gem)#
	gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
	curl -sSL https://get.rvm.io | bash -s stable
 *若沒有curl*
 
	#安裝curl#
	winpty apt update
	winpty apt upgrade
	winpty apt install curl
	curl --version ###看目前版本

`exit`
* 離開容器

`docker commit -m "m的內容" -a "a的內容" [用來建映像檔的容器ID] [新映像檔名跟tag]`
* 提交更新後的副本 (創了一個新的映像檔)
 >-m : 指令提交的說明信息
 -a : 指定更新的使用者信息

**利用docker commit擴展映像檔較簡單，但不方便在一個團隊中分享**
  solution : 利用docker build建立新映像檔
 
 首先創建一個Dockerfile `touch Dockerfile`
 >\# : 註釋
 FROM : 告訴docker使用哪個image作為基底
 MAINTAINER : 維護者信息
 RUN : 其指令會在建立中執行

