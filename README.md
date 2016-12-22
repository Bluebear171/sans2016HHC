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
- 找齊所有啟動Cranberry Pi的零件，找齊後他會給你Cranbian image，並且希望你能幫他找到Login的密碼。

零件的所在地:
- Cranberry Pi Board
- Power Cord
- HDMI Cable
- SD Card
- Heat Sink
