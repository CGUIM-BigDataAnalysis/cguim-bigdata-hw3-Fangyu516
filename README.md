長庚大學 大數據分析方法 作業三
================

網站資料爬取
------------

``` r
#這是R Code Chunk
library(rvest) ##第一次使用要先安裝 install.packages("rvest")
```

    ## Warning: package 'rvest' was built under R version 3.3.3

    ## Loading required package: xml2

    ## Warning: package 'xml2' was built under R version 3.3.3

``` r
pttmovie<-"https://www.ptt.cc/bbs/movie/index.html"

pttdata<-c()
for(n in 1:8){
  pttContent<-read_html(pttmovie)
  post_title <- pttContent %>% html_nodes(".title") %>% html_text()
  post_pushnum<- pttContent %>% html_nodes(".nrec") %>% html_text()
  post_author<- pttContent %>% html_nodes(".author") %>% html_text()
  
  pttmovie_posts <- data.frame(title = post_title, author=post_author, pushnumber=post_pushnum)
  pttdata<-rbind(pttdata,pttmovie_posts)
  
  pttpre<-read_html(pttmovie)%>% html_nodes(".btn-group-paging a:nth_child(2)") %>% html_attr("href")
  pttmovie<-paste0("https://www.ptt.cc",pttpre)
}
##read_html
##html_nodes
##html_text
```

爬蟲結果呈現
------------

``` r
#這是R Code Chunk
knitr::kable(
  pttdata[c("title","author","pushnumber")]) ##請將iris取代為上個步驟中產生的爬蟲資料資料框
```

| title                                                          | author       | pushnumber |
|:---------------------------------------------------------------|:-------------|:-----------|
| \[片單\] 類似"白雪公主殺人事件"的日本電影                      | somniloquy   | 5          |
| \[情報\]《大藝術家》導演執導「高達」傳記電影《Redoutable》預告 | qpr322       | 5          |
| \[好雷\] 攻殼機動隊觀後感                                      | blackone979  | 1          |
| \[好雷\]《目擊者》：台灣類型電影的成熟典範                     | ourstage     |            |
| \[公告\]《各式疑難雜症FAQ》                                    | yunyun85106  | 23         |
| \[公告\] 板規！必看！｜好文推薦‧惡文檢舉                       | ericf129     | 爆         |
| \[新聞\] 萊恩葛斯林不介意頒錯獎                                | MyAll        | 6          |
| \[普雷\] 聲之形                                                | st40182      | 9          |
| \[好雷\] 異星智慧 Life，人生呀                                 | mysmalllamb  | 2          |
| \[超好雷\]我和我的冠軍女兒                                     | koa777       | 8          |
| \[片單\] 求主角一人反殺的片~~                                  | phoebeshong  | 18         |
| \[無雷\] 看金剛戰士前的忠告                                    | Ebergies     | 3          |
| \[討論\] 話當年的香港電影(十三)青蛇                            | caro770880   | 10         |
| \[普雷\] 攻殼機動隊                                            | Beanoodle    | 6          |
| Re: \[情報\] 《正義聯盟》片長公佈！                            | alljerry04   | 13         |
| \[贈票\] 恐怖驚悚【逃出絕命鎮】北中南搶先看                    | ChloeD       | 爆         |
| \[請益\] 怎麼都沒人討論金剛戰士的置入                          | mustafar     | 4          |
| \[問片\] 一部應該是蠻久以前的災難片                            | ttps61304    |            |
| \[新聞\] 神鬼奇航5的評價出來了                                 | sonans       | 6          |
| \[好雷\] 攻殼機動隊IMAX3D（有雷）                              | Eddward      | 1          |
| \[好雷\] 金剛戰士出乎我意料之外的好看                          | t13thbc      | 1          |
| \[普負雷\] 攻殼機動隊 拿掉殼還剩什麼？                         | rainyamei    | 6          |
| \[好雷\] 攻殼機動隊                                            | Sam0907      | 7          |
| \[普雷\]《攻殼機動隊》-押井守的殼,好萊塢的Ghost                | jk10134      | 1          |
| Re: \[問片\] 精神疾病女主殺人裝箱                              | fmlpeter     | 2          |
| \[新聞\] 還在等什麼？地表最強團隊就差你一個！                  | ChloeD       |            |
| \[好雷\]奪魂鋸2 - 承先啟後的佳作                               | LittleDiDi   | 7          |
| \[ 雷\] 攻殼機動隊 Ghost in the Shell 2017                     | natalie0609  | 8          |
| \[情報\] 《正義聯盟》片長公佈！                                | rhappyd      | 69         |
| Re: \[討論\] BVS終極版 很神啊                                  | killua92     | 22         |
| \[超好雷\]《異星智慧》意外本周最好看                           | allshine     | 5          |
| \[選片\] 冠軍女兒、異星智慧、金剛戰士                          | linkcat      | 46         |
| \[討論\] 影星【邱淑貞】PK【女兒沈月】 誰比較美?                | psooolder    | 61         |
| Re: \[討論\] IT 小丑噩夢歸來 2017預告                          | playerd      |            |
| \[選片\] 「我的冠軍女兒」、「美女與野獸」                      | tonyjojo     | 21         |
| (本文已被刪除) \[Wall62\]                                      | -            |            |
| \[選片\] 多片選片                                              | tenminutes   | 18         |
| \[新聞\] 原來如此？！這個角色不會回歸【不可能的                | Wall62       | 15         |
| \[選片\] 金爆內幕與異星智慧                                    | yyaa         | 8          |
| \[好雷\] it follows (靈病) 一場詭異的惡夢                      | LeonDiCaprio | 8          |
| \[無雷\] 在馬來西亞看攻殼機動隊                                | fundgto1975  | 8          |
| \[退票\]關於信義威秀失火線上退票手續費                         | frlfm        | 5          |
| Re: \[請益\] DC的電影規劃是不是沒有很好阿?                     | ckshchen     | 18         |
| \[新聞\] 《蜘蛛人：返校日》不會把東尼與梅嬸湊對                | qn123456     | 16         |
| \[新聞\] 坎城影展新海報大咖女星也遭修圖                        | qpr322       | 3          |
| \[問片\] 找一部十幾年前的日本片                                | itiscool     | 3          |
| \[情報\] 我和我的冠軍女兒臺北票房                              | lovelandbird | 21         |
| \[新聞\] 韓版不能說的秘密明年開拍 網友不買單                   | iam168888888 | 25         |
| \[新聞\] 莊凱勛拍目擊者 認真相也許沒那麼重要                   | iam168888888 | 16         |
| \[普雷\] 金剛戰士 Power Rangers-追的是一段青春                 | practice24   | 6          |
| \[問片\] 找部年代久遠香港有紙紮人的鬼片(已找到)                | xxshoxx      | 5          |
| \[問片\]在FB看到的預告 日本電影(已找到)                        | cherish91173 | 12         |
| \[新聞\] 艾莉西亞薇坎德全新《古墓奇兵》首張劇照                | sampsonlu919 | 18         |
| \[新聞\] 【電影特稿】史上罕見首映火災 《目擊者                 | ghooh        | 4          |
| \[負雷\] 《攻殼機動隊》簡易心得                                | vollier      | 32         |
| \[討論\] IT 小丑噩夢歸來 2017預告                              | acer12356    | 15         |
| \[討論\] 泰瑞莎帕瑪主演【Berlin Syndrome】預告                 | sure0219     | 3          |
| \[負雷\] 可以更好的金剛戰士                                    | gca00631     | 2          |
| (本文已被刪除) \[Mib2004\]                                     | -            |            |
| (本文已被刪除) \[Mib2004\]                                     | -            | 4          |
| \[討論\] Coco & Ferdinand 預告                                 | bigalow      | 2          |
| \[有雷\] 霸凌者視角《聲之形》                                  | KevinMoleaf  | 2          |
| Re: \[討論\] BVS終極版 很神啊                                  | DarkerWu     | 18         |
| Re: \[請益\] DC的電影規劃是不是沒有很好阿?                     | MRsoso       | 36         |
| \[情報\]玩命關頭8 , 首映初步評價                               | lovemelissa  | 56         |
| \[請益\] 請問電影夜宴的小問題                                  | beebeebee    | 4          |
| (本文已被刪除) \[AirPenguin\]                                  | -            | 2          |
| Re: \[新聞\] 好萊塢片商：新片上映45天 開放在家隨選             | Tosca        | 6          |
| Re: \[討論\] 鋼鐵英雄的女主角                                  | denverkober  | 10         |
| \[討論\] 巴霍巴利官方臉書電影直播中！                          | shyuwu       | 3          |
| Re: \[討論\] 攻殼機動隊評價開爐                                | n99lu        | 22         |
| \[討論\] 怪獸與牠們的產地 小問題                               | MyAll        | 15         |
| \[討論\]Valerian 星際特工瓦雷諾新預告出來了                    | KYALUCARD    | 20         |
| \[新聞\] 【電影版聲之形】獲台灣聽障人士高度肯定                | kkaicd1      | 8          |
| \[討論\] 誠實預告: 怪獸與牠們的產地 (雷)                       | abani        | 5          |
| \[大負雷\] 金剛戰士(心得已補)                                  | kai0101      |            |
| \[討論\] 找詭異劇情驚悚片                                      | tusna08124   | 32         |
| \[片單\] 請推薦類似《王牌對王牌》的電影                        | BHrabal      | 9          |
| \[討論\] 攻敵必救 (雷)                                         | HellYeah     | 4          |
| \[翻譯\]電影能夠如何正確地「嚇人」                             | cgmagic7     | 9          |
| \[新聞\] 阿部寬訪台談出道30年「想回到初心再出發                | vupmp6       | 5          |
| \[問片\] 主角被關在一個地方                                    | gasby3487    | 1          |
| \[新聞\] 他是昔日的「綠衣戰士」大明　卻在《金剛                | chocoball    | 12         |
| \[好雷\]Dangal【我和我的冠軍女兒】心得—既是冠軍，更是女兒      | FingerBender | 17         |
| \[？雷\] 攻殼機動隊                                            | Zeel         | 5          |
| \[爆好雷\] 密探心得（外加疑問）                                | yuka0117     | 3          |
| \[討論\] 猜火車2 四場加場再次秒殺                              | KYLAT        | 48         |
| Fw: \[閒聊\] 《金剛狼是狼嗎？》                                | rick0905     | 35         |
| \[新聞\] 這項成就 讓史特龍與卓別林齊名                         | leemz        |            |
| \[好雷\] 聲之形 改編劇本的成功                                 | filmania     | 17         |
| \[討論\] 如果找館長跟豆導來演美女與野獸會怎樣                  | goodgooddad  | 4          |
| Re: \[討論\] BVS終極版 很神啊                                  | vin00        | 8          |
| \[問片\] 宮女寫莫待無花空折枝給阿哥                            | whiterM      | 1          |
| (本文已被刪除) <mimi8598>                                      | -            | 48         |
| \[問片\] 警察的冤獄?                                           | s4028600     | 8          |
| \[討論\] 《愛是您愛是我》續集短片（中文字幕）                  | AceRocker    | 55         |
| (本文已被刪除) \[loveponpon\]                                  | -            |            |
| \[情報\] 無敵破壞王2:Ralph Breaks the Internet                 | tonyh24613   | 31         |
| \[請益\] 我和我的冠軍女兒疑問                                  | wij51271     | 8          |
| \[問片\] 韓國犯罪片 真實改編(已解決                            | arhtur945    | 12         |
| Re: \[討論\] BVS終極版 很神啊                                  | rapnose      | 5          |
| \[好雷\]《小鎮醫生》-沙漠中的橘井，荒原中的杏林                | jk10134      |            |
| \[贈票\] 今晚1910西門國賓 攻殼機動隊（已送出                   | tf310244     | 7          |
| \[問片\] 找日本電影，女主救一直死掉的同學                      | TTSENG10     | 13         |
| \[新聞\] 《不能說的秘密》翻拍韓版！                            | OGC789456123 | 44         |
| \[新聞\] 好萊塢片商：新片上映45天 開放在家隨選                 | asd591922    | 58         |
| \[新聞\] 丹史蒂文斯飾演查爾斯狄更斯傳記                        | sampsonlu919 | 6          |
| \[新聞\] 阿部寬登台無人接機喊糗 自爆怪癖塞3年鞋                | sarada       | 25         |
| Re: \[閒聊\] 搞不懂梁朝偉演技到底哪裡好                        | MRsoso       | 43         |
| \[ 好雷\] 險路勿進，no country for old man                     | roliproject  | 39         |
| Re: \[新聞\] 正義聯盟英雄雲集 關鍵人物竟是「他                 | ClawRage     | 5          |
| Re: \[負雷\]星際過客 爛到氣                                    | Verola       | 6          |
| \[請益\] 有人原本討厭但看完金剛戰士改觀的嗎                    | phantom78626 | 13         |
| \[請益\] 電影的片長是有包括片尾的演員表嗎？                    | poeta        | 10         |
| (本文已被刪除) \[zkow\]                                        | -            |            |
| \[討論\] 攻殼機動隊評價開爐                                    | takura       | 64         |
| \[好雷\] Dangal《我和我的冠軍女兒》- 不只是金牌                | pttpttlin    | 16         |
| \[好雷\] 沉默                                                  | cheerking    | 12         |
| \[問片\] 關於內褲的電影                                        | noending5423 | 4          |
| (本文已被刪除) \[sfzerox\]                                     | -            |            |
| \[好雷\] 金剛戰士 POWER RANGERS                                | sfzerox      | 20         |
| Re: \[討論\] BVS終極版 很神啊                                  | aspired      | 8          |
| \[討論\] 無處可逃                                              | atoa14       | 9          |
| \[問片\] 一部有年代的日本電影                                  | slazengerfig | 2          |
| \[ 好雷\] 英雄電影的新路線，羅根                               | roliproject  | 3          |
| \[討論\] 為何迪士尼公主系列沒有寶嘉康蒂                        | ivycheng0415 | 39         |
| \[普雷\] 父權下的女權-我和我的冠軍女兒                         | bluexebec    | 15         |
| \[新聞\] "萬磁王"配"瘋眼"【犯罪教條】再續父子情                | kkaicd1      | 6          |
| \[選片\] 攻殼機動vs傷物語vs黑色追緝令vs寶貝老闆                | Emerson158   | 12         |
| \[討論\]【蜘蛛人：返校日】最新預告                             | dragon50119  | 爆         |
| \[新聞\] 玩命再劫導演不要命 為抓鏡頭跟著飛車                   | iam168888888 |            |
| \[新聞\] 韓電影在陸吃閉門羹 北京影展拒播映                     | iam168888888 | 11         |
| \[討論\] 片名直接爆雷不永桶片商嗎?                             | NiNiHOT      |            |
| Re: \[請益\] 我和我的冠軍女兒                                  | iseedeadman  |            |
| Re: \[贈票\] 湯姆漢克斯大力推薦《衝突的一天》贈票              | pelicula     | 2          |
| (本文已被刪除) <Hekomi>                                        | -            |            |
| \[好雷\]《最後的詩句》：有一塊壁癌很明顯                       | dilovewia    | 8          |
| \[問片\] 問一部小時候看的科幻片(有雷)                          | TITITTI      | 3          |
| Re: \[討論\] BVS終極版 很神啊                                  | windr        | 29         |
| \[討論\] 兇手正在看著你(The Watcher)                           | liu2007      | 1          |
| \[低能雷\] 異星智慧是一部嚴重種族歧視的片                      | vaiking0120  | X1         |
| \[好雷\] 我和我的冠軍女兒                                      | tkps21       | 18         |
| 〔問片〕 二十年前的國片                                        | hopeless     | 4          |
| \[片單\] 請推薦演員讓人覺得很變態、神經質的片                  | st264201     | 爆         |
| \[新聞\] 正義聯盟英雄雲集 關鍵人物竟是「他」？                 | sampsonlu919 | 6          |
| \[新聞\] 詹姆斯岡恩透露《星際異攻隊2》開頭將會                 | Wall62       | 4          |

解釋爬蟲結果
------------

``` r
str(pttdata)
```

    ## 'data.frame':    146 obs. of  3 variables:
    ##  $ title     : Factor w/ 139 levels "\n\t\t\t\n\t\t\t\t[公告] 板規！必看！｜好文推薦‧惡文檢舉\n\t\t\t\n\t\t\t",..: 3 6 4 5 2 1 21 16 11 19 ...
    ##  $ author    : Factor w/ 125 levels "blackone979",..: 5 4 1 3 6 2 17 23 18 15 ...
    ##  $ pushnumber: Factor w/ 41 levels "","1","23","5",..: 4 4 2 1 3 5 12 15 9 14 ...

``` r
table(pttdata$author)
```

    ## 
    ##  blackone979     ericf129     ourstage       qpr322   somniloquy 
    ##            1            1            1            2            1 
    ##  yunyun85106   alljerry04    Beanoodle   caro770880       ChloeD 
    ##            1            1            1            1            2 
    ##     Ebergies      Eddward     fmlpeter      jk10134       koa777 
    ##            1            1            1            2            1 
    ##     mustafar        MyAll  mysmalllamb  phoebeshong    rainyamei 
    ##            1            2            1            1            1 
    ##      Sam0907       sonans      st40182      t13thbc    ttps61304 
    ##            1            1            1            1            1 
    ##            -     allshine     ckshchen        frlfm  fundgto1975 
    ##            9            1            1            1            1 
    ##     itiscool     killua92 LeonDiCaprio      linkcat   LittleDiDi 
    ##            1            1            1            1            1 
    ##  natalie0609      playerd    psooolder     qn123456      rhappyd 
    ##            1            1            1            1            1 
    ##   tenminutes     tonyjojo       Wall62         yyaa    acer12356 
    ##            1            1            2            1            1 
    ##    beebeebee      bigalow cherish91173     DarkerWu     gca00631 
    ##            1            1            1            1            1 
    ##        ghooh iam168888888  KevinMoleaf lovelandbird  lovemelissa 
    ##            1            4            1            1            1 
    ##       MRsoso   practice24 sampsonlu919     sure0219      vollier 
    ##            2            1            3            1            1 
    ##      xxshoxx        abani      BHrabal     cgmagic7    chocoball 
    ##            1            1            1            1            1 
    ##  denverkober FingerBender    gasby3487     HellYeah      kai0101 
    ##            1            1            1            1            1 
    ##      kkaicd1    KYALUCARD        n99lu       shyuwu        Tosca 
    ##            2            1            1            1            1 
    ##   tusna08124       vupmp6     yuka0117         Zeel    AceRocker 
    ##            1            1            1            1            1 
    ##    arhtur945    asd591922     filmania  goodgooddad        KYLAT 
    ##            1            1            1            1            1 
    ##        leemz OGC789456123      rapnose     rick0905     s4028600 
    ##            1            1            1            1            1 
    ##     tf310244   tonyh24613     TTSENG10        vin00      whiterM 
    ##            1            1            1            1            1 
    ##     wij51271      aspired       atoa14    cheerking     ClawRage 
    ##            1            1            1            1            1 
    ## ivycheng0415 noending5423 phantom78626        poeta    pttpttlin 
    ##            1            1            1            1            1 
    ##  roliproject       sarada      sfzerox slazengerfig       takura 
    ##            2            1            1            1            1 
    ##       Verola    bluexebec    dilovewia  dragon50119   Emerson158 
    ##            1            1            1            1            1 
    ##     hopeless  iseedeadman      liu2007      NiNiHOT     pelicula 
    ##            1            1            1            1            1 
    ##     st264201      TITITTI       tkps21  vaiking0120        windr 
    ##            1            1            1            1            1

總共有145篇文章, iam168888888最多發文

``` r
#這是R Code Chunk
```

解釋解釋解釋解釋

我發現鄉民會在pttmovie版透過一些訊息請大家幫忙尋找電影名稱
