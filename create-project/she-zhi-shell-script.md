# 設置 Shell Script

#### 建立腳本檔案

名字隨意，取一個打幾個字按 tab 就可以的名字為佳。（ 以下這個名字是不好的例子 ）

```sh
vim create-frontend-template.sh 
```

#### 撰寫內容

[http://gitlab.sltung.com.tw/frontend/frontend-template/-/wikis/Shell-Script-of-Create-Frontend-Project](http://gitlab.sltung.com.tw/frontend/frontend-template/-/wikis/Shell-Script-of-Create-Frontend-Project)

#### 為腳本檔案添加可執行權限

```sh
chmod +x create-frontend-template.sh 
```

#### 將腳本移至系統可執行的位置

```sh
sudo mv create-frontend-template.sh /usr/local/bin/

# 完成後，你可以在命令行中直接運行腳本，而無需在腳本名稱前面添加 ./

create-frontend-template.sh
```
