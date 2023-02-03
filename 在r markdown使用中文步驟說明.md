在r markdown使用中文步驟說明
--------
--------


**步驟一:環境設置**

在r studio中使用以下指令安裝套件"rticles"

    install.packages("rticles")

此套件會讓R studio中可選擇的R Markdown模板增加，我們需要的就是其中一個模板，詳情請看[rticles github](https://github.com/rstudio/rticles)。

--------

**步驟二，創建一個模板**

選取file>New file>R Markdown

![graph1](![1](https://user-images.githubusercontent.com/38903695/216540143-6d6c433f-66a1-4742-9e16-4b9009db4c4e.png)
)


之後會跳出以下畫面，選擇From Template，之後選擇CTeX Documents

![graph2](![2](https://user-images.githubusercontent.com/38903695/216540191-d68c0e79-e2ed-4955-93a9-2f0c4320526b.png)
)


完成後即可生成以下模板，就可以使用簡體中文了

![graph3](![3](https://user-images.githubusercontent.com/38903695/216540276-001162de-359c-46ba-84d3-f46fe55f561d.png)
)

--------

**步驟三 將環境改為繁體中文**

由於該套件作者使用的是簡體中文，因此如果要使用繁體中文還需要給文件一些追加設定，追加設定的方法就是在rticles::cex:後面追加一行include:in_header:setup.tex，並且把這個setup.tex放到和rmd檔同樣的資料夾內。

![graph4](![4](https://user-images.githubusercontent.com/38903695/216540297-e7b57af1-d5d3-42bf-85d9-2c5cc4d41cf3.png)
)


這行指令的功能是在生成tex檔時，額外給他一些設定，不過要注意，給的額外設定不可以和原始設定衝突，因此若要自行新增其他設定請記得跑一次模板，然後看看產生的tex檔內有什麼東西。
繁體中文設定的setup.tex請參考[附件tex檔](http://140.116.52.106/miaoyu/r-markdown-chinese-1/-/blob/master/setup.tex)。

--------


**其他說明1:如何知道自己硬體內有甚麼字體?**


*  自己電腦:

叫出cmd，然後使用以下指令

    fc-list :lang=zh

*  查server上的硬體:

叫出自己電腦的cmd，然後用以下指令先登入server的cmd，之後使用上述一樣的指令。

    ssh [username]@[server id]


即可如下圖列出自己電腦或server上有的字體(註:這是window系統的指令)

![graph5](![5](https://user-images.githubusercontent.com/38903695/216540337-43ffc50e-175f-46a3-ae5e-764c3d3ebe5a.png)
)

以上圖為例，如果我想使用新細明體，則可以在setup.tex字體中指定"新細明體"或是"PMingLiU"來呼叫此字體

--------
**其他說明2:如何在r markdown中使r package "Hmisc" 輸出的敘述統計包含直方圖**

在setup.tex中，需要用以下指令來使用setspace、relsize這兩個package。

    \usepackage{setspace,relsize}

在r markdown中使用以下指令。

    ```{r describe, results='asis'}
    latex(describe(iris, descript = "鳶尾花敘述統計"), file = "", caption.placement = "top")
    ```

results='asis'的意思是以原本樣子去做輸出(原本在r markdown 直接print文字他會自動在文字前多加兩個##)

latex(describe)則是把這段輸出結果直接改成latex語法

歡迎參考[範例檔案](http://140.116.52.106/miaoyu/r-markdown-chinese-1/-/blob/master/sample.Rmd)。

--------
