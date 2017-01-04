# SANS2016HHC

This is the writeup on how I solve the 2016 SANS Holiday Hack Challege

## Table of Contents
1. Introduction
2. Part 1: A Most Curious Business Card
3. Part 2: Awesome Package Konveyance
4. Part 3: A Fresh-Baked Holiday Pi
5. Part 4: My Gosh... It's Full of Holes
6. Part 5: Discombobulated Audio
7. Appendex
 - 7.1 Character Dialog History
 - 7.2 Achievement
 - 7.3 Oraganised Answer

### Introduction
故事發生在一個夜深人靜的晚上，喬斯(Josh Doise)和傑西卡(Jessica Doise)在睡覺的時候聽到聖誕老人竟然出現在他們家裡的聲音。但正當他們決定要去看看聖誕老人的真面目時，發生了一些十分奇怪的事情，一陣禮物被撕破的聲音從他們家樓下傳出來。他們還聽到尖銳的打鬥聲，很可惜的是，在他們去到樓下時候，聖誕老人已經不見了，只見到家裡一片混亂，家裡的聖誕樹還甚至被劈開一半呢。為了調查事件的發生你們將開始一段新的冒險。在我進入遊戲教程前，我想先說這個遊戲裡面所有的挑戰都是他們設計的：
- Mark Baggett
- Tad Bennett
- Ron Bowes
- Jeff McJunkin
- Tim Medin
- Lee Neely
- Ed Skoudis
- Joshua Wright

在這裡感謝他們設計的挑戰讓我學到新的Forensic知識。想進入遊戲挑戰自己的人可以按[這裡](https://quest2016.holidayhackchallenge.com/)

### Part 1:A Most Curious Business Card

[![venue1.jpg](https://s29.postimg.org/88tfwhkjr/venue1.jpg)](https://postimg.org/image/6h0h1l16r/)

遊戲一開始你就會身處在聖誕老人不見了的案發現場。在和喬斯和傑西卡對話後，你知道你需要調查那張留在現場神秘的卡片。這張卡片留下了聖誕老人的Twitter戶口以及Instagram戶口。

[![santawclaus_shadow.png](https://s29.postimg.org/69cik10ef/santawclaus_shadow.png)](https://postimg.org/image/44s5ixyrn/)

仔細調查後，你可以發現到聖誕老人的Tweet隱藏着其他信息。如果想快速獲取聖誕老人留下的所以信息你可以用tweet_dumper.py，一次過將所有對話save成CSV文件。當你成功把所有對話都整齊排列好你會看到所有的信息會組成一個很大而且明顯的信息，那就是:BUGBOUNTY。

你也可以在http://twlets.com/ 這個網站直接將自己或他人Twitter的信息變成CSV文件。
[![bugbunty.jpg](https://s23.postimg.org/xsrti039n/bugbunty.jpg)](https://postimg.org/image/ik1w489l3/)

接著你可以查看聖誕老人的Instagram，在第一張照片找到了2個Zip File的提示。

[![Insta.jpg](https://s23.postimg.org/aq25xsut7/Insta.jpg)](https://postimg.org/image/lpnd9el87/)

- 提示1：電腦上出現了Zip file的名字：SantaGram_v4.2.zip
- 提示2：紙張上有這個網站http://www.northpolewonderland.com/

憑著這兩個提示你可以聯想到的是Zip File的位置可能就是:http://www.northpolewonderland.com/SantaGram_v4.2.zip 。經過嘗試後你就會成功下載到那個Zip File。裡面有一個SantaGram_4.2.apk的文件。

### Part 2:Awesome Package Konveyance
[![Holly.jpg](https://s24.postimg.org/t3kwc4rad/Holly.jpg)](https://postimg.org/image/fzfbzfz8h/)

接下來的故事發展，你會通過一個禮物袋來到一個冰天雪地的地方。沒錯，這裡就是聖誕老人和他的精靈居住的地方，北極。這時候你會見到Holly Evergreen。他會告訴你以下幾件事情：
- 在你去攻擊任何一個系統之前，請先去拜訪Oracle。
- Santagram 是聖誕老人和他的精靈所使用的社交媒體，想知道更多可以去拜訪在北極的其他精靈哦。
- 找齊所有啟動Cranberry Pi的零件，找齊後他會給你Cranbian image，並且希望你能幫他找到Login的密碼。[詳細資料請參考Part 3]

零件的所在地:[以後補充]
- Cranberry Pi Board
- Power Cord
- HDMI Cable
- SD Card
- Heat Sink

[![Shinny Uptree.jpg](https://s23.postimg.org/7zo277wor/Shinny_Uptree.jpg)](https://postimg.org/image/7mwo11eev/)

為了找回失踪的聖誕老人，你必須想辦法去知道Santagram_4.2.apk 這個文件裡面到底隱藏了什麼信息。在北極尋找了一段時間後，你可以在聖誕老人工作室的火車站找到Shinny Upatree。他會告訴你怎樣去分析你找到的APK文件。從他口中你明白到了以下的事情：
- APK File 也是Zip File的一種你可以Unzip來取得裡面的所有文件。
- APK File 是用Java程式語言來寫，想找回原本的Coding，要用Android Studio 或者JadX 來Decompile那個APK File。
- Jadx commandline可以將APK file Decompile成每一個獨立的Java文件。
- Joshua在2016Hack Fest呈現的[簡報](https://goo.gl/m076lb)裡面也有提及如何更有效的使用Android Studio and JadX來分析Apk文件。

得到這些有用的情報後，你可以開始分析你得到的Apk文件了。正當你Unzip的時候發覺你需要輸入密碼才能繼續你的分析，不然你就無法繼續下去。其實，我在解題的時候在這裡卡了很久的一段時間，直到我在Reddit那邊見到有一個人給予的提示：你可能已經一早獲得了Unzip Santagram的密碼，只是你自己沒察覺到而已。我腦中醒起會不會是之前的BUGBOUNTY。最後，皇天不負有心人，我成功找到密碼(bugbounty)啦。進入分析Apk的階段，你可以用JadX 去Decompile 你得到的Apk文件，一旦Jadx成功Decompile後，你就能找題目要求你的username and password。使用Text Search功能你可以找到username and password 都隱藏在Code裡面。這段Code你可以在northpolewonderlad.santagram.SplashScreen Class裡面找到。

[![userpass.jpg](https://s28.postimg.org/4gi5nv3gt/userpass.jpg)](https://postimg.org/image/dbizyds95/)

`jSONObject.put("username", "guest");
 jSONObject.put("password", "busyreindeer78");
`

另外，題目要求的Audio Component你可以在res/raw裡面找到，文件名稱為：discombobulatedaudio1.mp3。Unzip Santagram的Apk你也可以的直接得到該Mp3 File。

`unzip Santagram_4.2.apk`

如果想要該Mp3文件，可以到這裡[下載](https://drive.google.com/open?id=0B18u7ECQO-gTLTUteDQ4ZDZsdkk)

### Part 3: A Fresh-Baked Holiday Pi
在解決了apk的文件後，你終於可以靜下心來研究一下你剛剛得到的Cranbian image。要知道怎樣使用這個Image你可以找在聖誕樹下的Wunhorse Openslae來詢問。從他口中你明白到了以下的事情：
- Cranbian 其實是Linux Based的File System Image。
- Eskoudis 的部落格會教你[如何Mount a Raspberry Pi File System Image](https://pen-testing.sans.org/blog/2016/12/07/mount-a-raspberry-pi-file-system-image)

當你Unzip disk image後，你可以按照以下步驟來打開Cranbian image。
- Step 1:用`fdisk -l cranbian-jessie.img`command你可以得知這個Image由2個部分組成。而你要找的資料是在第二個部分裡面。你也會知道開始的Sectors會是137216。
- Step 2:由於mount command需要用到Offset，所以你要計算出Offset的總值得。這個Image的offset=512×137216=70254592
- Step 3:打`mount -v -o offset=70254592 -t ext4 cranbian-jessie.img mnt/` 你就能成功Mount Cranbian Image.
  
