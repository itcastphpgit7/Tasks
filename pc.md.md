### 什么是爬虫

爬虫：一段自动抓取互联网信息的程序，从互联网上抓取对于我们有价值的信息；

 

Python爬虫架构：
Python爬虫架构主要由五个部分组成，分别是 调度器、URL管理器、网页下载器、网页解析器、应用程序（爬取的有价值数据）

1）调度器：
相当于一台电脑的CPU，主要负责调度URL管理器、下载器、解析器之间的协调工作；

2）URL管理器：
包括待爬取的URL地址和已爬取的URL地址，防止重复抓取URL和循环抓取URL，实现URL管理器主要用三种方式：通过内存、数据库、缓存数据来实现；

3）网页下载器：
通过传入一个URL地址来下载网页，将网页转换成一个字符串，网页下载器有urllib（Python官方基础模块），包括需要登录、代理和Cookie；还有requests（第三方包）；

4）网页解析器：
将一个网页字符串进行解析，可以按照我们的要求来提取出我们有用的信息，也可以根据DOM树的解析方式来解析；

网页解析器有：

1）正则表达式：

  直观，将网页转成字符串通过模糊匹配的方式来提取有价值的信息；

  但当文档比较复杂的时候，该方法提取数据的时候就会非常困难；

2）html.parser：Python自带的；

3）beautifulsoup：第三方插件，可以使用Python自带的html.parser进行解析，也可以使用lxml进行解析；

4）lxml：第三方插件，可以解析xml和HTML；

html.parser和beautifulsoup，以及lxml都是以DOM树的方式进行解析的；

5）…

5）应用程序：
就是从网页提取的有用数据组成的一个应用；

调度器工作图解：



示例：
urllib实现下载网页内容：（PY3）

\#!/usr/bin/python
\# -*- coding:utf-8 -*-

import urllib.request
import urllib

url = '![img](file:///C:\Users\86177\AppData\Roaming\Tencent\QQTempSys\[5UQ[BL(6~BS2JV6W}N6[%S.png)http://www.baidu.com'
response = urllib.request.urlopen(url)
content = response.read().decode('utf-8')
print(content)
（content是html文档太长就不附在这里了）\#!/usr/bin/python
\# -*- coding: UTF-8 -*-

import requests
from bs4 import BeautifulSoup

movie_url = '![img](file:///C:\Users\86177\AppData\Roaming\Tencent\QQTempSys\8LDO48C$8@[GWU0353$FOVS.png)https://movie.douban.com/subject/1292052/'

def download_page(url):
	headers = {
	'User-Agent':'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_12)AppleWebKit/537.36 (KHTML, like Gecko) Chrome/47.0.2526.80 Safari/537.36'
	}

​	data = requests.get(url, headers = headers).content
​	return data

def paser_html(html):
	soup = BeautifulSoup(html, 'lxml')
	title = soup.find(property = 'v:itemreviewed').string

​	return title

def main():
	print(paser_html(download_page(movie_url)))


if __name__ == '__main__':==-main-

#coding=utf-8


import json
import demjson
import urllib2
import os
import time
import requests
import re
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.support.wait import WebDriverWait
import sys
reload(sys)
sys.setdefaultencoding('utf8')

path_name = u'T恤宽松日系男款'  #图片保存的文件夹名称
Myname = u'T恤宽松日系男款'   #搜索关键字

创建文件夹

path = os.getcwd()   				     # 获取此脚本所在目录
new_path = os.path.join(path,path_name)
if not os.path.isdir(new_path):
	os.mkdir(new_path)

#url请求，获取响应的json数据，并将json数据转换成dict  采用selenium实现
def get_browser_text(url):
    #browser = webdriver.Chrome(executable_path="C:\\Program Files (x86)\\Google\\Chrome\\Application\\chromedriver.exe")
    browser = webdriver.Firefox(executable_path="C:\\Program Files (x86)\\Mozilla Firefox\\geckodriver.exe")
    try:
        browser.get(url)
        print(browser.page_source)
        browserdata = browser.page_source
        browser.close()
        # res = r'<a .*?>(.*?)</a>'
        res = r'<pre .*?>(.*?)</pre>'
        json_data = re.findall(res, browserdata, re.S | re.M)
        print json_data
        for value in json_data:
            print value

        dict_data = demjson.decode(json_data)
        print 'dict_data:'
        print dict_data
        # print type(dict_data)
        return dict_data
    except:
        return ""

 



#url请求，获取响应的json数据，并将json数据转换成dict  采用 urllib2 实现
def getJSONText(url):
    try:
        page = urllib2.urlopen(url)
        data = page.read()
        #print (data)
        #print (type(data))
        #dict_data = json.loads(data)
        dict_data = demjson.decode(data)
        #print dict_data
        #print type(dict_data)
        return dict_data
    except:
        return ""

获取单个商品的HTML代码并用正则匹配出描述、服务、物流3项参数  采用urllib2

def getHTMLText(url):
    try:
        data = urllib2.urlopen(url).read()
        res = r'<dd class="tb-rate-(.*?)"'
        data_list = re.findall(res, data, re.S | re.M)
        print type(data_list)
        print data_list[0]
        #for value in mm:
        #   print value
​        return data_list
​    except:
​        return  ""


#url请求，获取响应的json数据，并将json数据转换成dict  采用 添加请求头、设置代理的方式 实现
def getJSONText2(url):
    try:
        proxies = {
            "http": "http://221.10.159.234:1337",
            "https": "https://60.255.186.169:8888",
        }
        headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36'}
        data = requests.get(url, headers=headers,proxies=proxies).text
        print (data)
        print (type(data))
        # dict_data = json.loads(data)
        dict_data = demjson.decode(data)
        print dict_data
        print type(dict_data)
        return dict_data
    except:
        return ""


def getJSONText3(url):
    try:
        driver = webdriver.Chrome(executable_path = "C:\\Program Files (x86)\\Google\\Chrome\\Application\\chromedriver.exe")
        driver.get(url)  # 访问淘宝宝贝页面，获取cookie
        # driver.get(taobao_comment_url)  # 直接访问宝贝评论会被反爬虫检测到。上一步获得cookie后可得到评论数据
        print(driver.find_element_by_xpath('/html/body').text)
        data = driver.find_element_by_xpath('/html/body').text
        #data = requests.get(url, headers=headers,proxies=proxies).text
        print (data)
        print (type(data))
        # dict_data = json.loads(data)
        dict_data = demjson.decode(data)
        print dict_data
        print type(dict_data)
        return dict_data
    except:
        return ""


def mytaobao_spider():
    # 每一页的url  循环抓取60页
    for page in range(0, 60):

        url = (
        'http://pub.alimama.com/items/search.json?q=%s&_t=1531556288035&toPage=%d&perPageSize=50&auctionTag=&shopTag=yxjh&t=1531556427336&_tb_token_=7e73deef30e18&pvid=10_117.136.70.61_599_1531556285246' % (
        Myname, page))
        # url = ('http://pub.alimama.com/items/channel/qqhd.json?q=%s&channel=qqhd&_t=1531121449018&toPage=%d&perPageSize=50&shopTag=&t=1531125125414&_tb_token_=eeee6ee3be688&pvid=19_118.112.188.32_688_1531125125232'%(Myname,page))
        # url = ('http://pub.alimama.com/items/search.json?q=%E9%9E%8B%E5%AD%90&_t=1531368912715&auctionTag=&perPageSize=50&shopTag=yxjh&t=1531368913289&_tb_token_=e370663ebef17&pvid=10_118.112.188.32_9532_1531368912863')
        print url
        time.sleep(2)  # 延时2秒，添加延时操作是因为淘宝有反爬虫机制，过于频繁的访问IP可能会被限制
        url_data = getJSONText(url)
        # 一页中每件商品的标签信息
        for i in range(0, 50):
            time.sleep(1)
            try:
                # print type(url_data['data']['pageList'][i]['pictUrl'])
                pictUrl = url_data['data']['pageList'][i]['pictUrl']  # 图片url
                sellerId = url_data['data']['pageList'][i]['sellerId']  # 商品id
                auctionUrl = url_data['data']['pageList'][i]['auctionUrl']  # 淘宝链接
                auctionId = url_data['data']['pageList'][i][
                    'auctionId']  # 淘宝链接 =  'http://item.taobao.com/item.htm?id=%d'%(auctionId)
                tkRate = url_data['data']['pageList'][i]['tkRate']  # 比率
                zkPrice = url_data['data']['pageList'][i]['zkPrice']  # 价格
     
                # 需要抓取比率大于10.00的商品信息
                if tkRate > 10.00:
                    # time.sleep(1)
                    # print '详细信息:'
                    # print type(tkRate)
                    # print type(zkPrice)
                    # print '比率:%f' % (tkRate)
                    # print '价格:%f' % (zkPrice)
                    # print sellerId
                    # print auctionId
                    # print pictUrl
                    # print auctionUrl  # 淘宝链接
                    # print type(sellerId)
                    print auctionUrl
     
                    # 每件商品的子url (描述相符、发货速度、服务态度 等信息)
                    # sub_url = ('http://pub.alimama.com/pubauc/searchPromotionInfo.json?oriMemberId=%d&blockId=&t=1531369204612&_tb_token_=e370663ebef17&pvid=10_118.112.188.32_760_1531368931581' % (sellerId))
                    sub_url = auctionUrl  # 每件商品的淘宝url
                    sub_url_data = getHTMLText(sub_url)  # 获取店铺的 描述、服务、物流 信息
                    print type(sub_url_data)
                    print len(sub_url_data)
     
                    # 如果返回的是空字符串, 则说明没有取到我们想要的字段，是因为淘宝有不同的页面，对于这种页面我们需要进一步分析下面的url
                    if (len(sub_url_data) == 0):
                        info_url = ('https://world.taobao.com/item/%d.htm' % (auctionId))
                        info_data = urllib2.urlopen(info_url).read()
                        res_info = r'<li class="([^s].*?)<img'
                        tmp_url_data = re.findall(res_info, info_data, re.S | re.M)
                        print "tmp_url_data:"
                        for value1 in tmp_url_data:
                            print value1
     
                        sub_url_data = []
                        score_list = [x[0:4] for x in tmp_url_data]  # 截取前面5位
                        print 'new_list:'
                        for score in score_list:
                            print score
                            if score == 'down':
                                score = 'lower'  # d第一种页面与第二种页面返回的店铺评定信息不同，需转换成统一的方便后面处理，将 down 转换为 lower
                            sub_url_data.append(score)
     
                        print '替换后的list元素:'
                        for level_data in sub_url_data:
                            print level_data
                    # 如果3项评定参数都不是‘lower’ 就将图片和相关信息抓取出来   任意一项参数为‘lower’都不符合要求
                    if ((not (sub_url_data[0] == 'lower')) and (not (sub_url_data[1] == 'lower')) and (
                    not (sub_url_data[2] == 'lower'))):
                        # for value in sub_url_data:
                        #   print value
     
                        mypictUrl = 'http:' + pictUrl  # 图片url
                        picture_content = urllib2.urlopen(mypictUrl).read()
                        picture_name = auctionUrl + '.jpg'  # 拼接图片名称
                        print picture_name
                        time.sleep(1)
     
                        # 需要写入文件的信息
                        spider_info = 'url:' + url + '\n' + '  sub_url:' + sub_url + '\n' + '  淘宝链接:' + auctionUrl + '\n' + '  mypictUrl:' + mypictUrl + '\n\n'
                        try:
                            # 写图片
                            index_num = picture_name.index('id=')
                            with open(path_name + '/' + picture_name[index_num:], 'wb') as code:
                                code.write(picture_content)
                            # 写URL信息
                            with open(path_name + '/' + 'spider.txt', 'a') as spider_code:
                                spider_code.write(spider_info)
                        except (IOError, ZeroDivisionError), e:
                            print e
                            print "Error: 没有找到图片文件或读取文件失败"
                        else:
                            print "图片写入成功"
     
                        time.sleep(1)
     
            except (IndexError, KeyError, TypeError), e:
                print e
                print "每件商品信息读取失败"
            else:
                pass
                # print "每件商品的标签信息读取成功"

 



if __name__ == '__main__':
    mytaobao_spider()



#### 爬虫小结

 网络爬虫（又被称为网页蜘蛛，网络机器人，在FOAF社区中间，更经常的称为网页追逐者），是一种按照一定的规则，自动地抓取万维网信息的程序或者脚本。通俗一点说就是爬取某个网站上的你想要的某些数据，然后保存起来。

   爬虫主要使用的是java和python语言，java语言是Python语言写爬虫的最大竞争对手。Python与java相比有很多优点，利用python写爬虫程序比较简洁，高效。python含有第三方urllib库，一个最基本的网络请求库，是用来写爬虫的好工具。学习用Python语言爬虫必须要对python的基本语法规则要有一定的了解。我在大一寒假的时候学习过python语言的一些基本语法知识，当时还照着书做过一个用python语言写的游戏。差不多都一年半没碰过python语言，我在图书馆找了一本《一天学会python》的书，用了两个多小时看完了，对Python语言的一些基本语法规则及使用更加熟悉了。然后我就开始了我的爬虫之旅。

开始爬虫之前有些基础知识必须知道，这些知识是爬虫必须知道的基础知识：

1、http协议：超文本传输协议，一种发布和接收HTML页面的方法，80端口，浏览器一般默认的都是80端口

2、https协议：http协议的加密版本，在http下加入ssl层，443端口

3、URL详解：统一资源定位符（就是浏览器上方的网址）一个URL一般由以下几个部分组成：

scheme：//host:port/path/?query-sting=xxx#anchor

scheme:协议一般为http、https、ftp

host:主机名或者域名例如![img](file:///C:\Users\86177\AppData\Roaming\Tencent\QQTempSys\[5UQ[BL(6~BS2JV6W}N6[%S.png)www.baidu.com或者IP地址，域名是IP地址的简称

port：端口号，浏览器一般默认80端口

path：查找路径

query-sting=xxx:查询字符串例如wd=python

anchor:锚点，前端用来做页面定位

在浏览器中请求一个URL，浏览器会对URL进行一个编码，除英文，数字和部分符号外，其他的全部使用百分号+十六进制码值进行编码。在urllib库里面有urlencode()函数对中文，符号进行编码，parse_qs()函数对中文、符号进行解码。

4、http常用请求方法：

post:向服务器发送数据、上传数据，对服务器产生影响

get:只能从服务器获取数据，不会对服务器产生影响

http请求方法详解

5、http协议常见响应状态码

200： 请求正常，服务器正常返回（数据不一定正确）

301：永久重定向

302：临时重定向

400：请求的URL找不到，URL错误

403：服务器拒绝访问

404：not found

500：内部服务器错误

更多http协议状态码

6、http协议请求头常见参数

在http协议中向服务器发送一个请求数据分为三部分，第一部分把数据放在url中，第二部分把数据放在body中，第三部分把数据放到head中。

user-agent:浏览器名称

referer:表明当前这个请求从哪个url过来

cookie：http协议是无状态的

7、爬虫协议

用爬虫爬取网站，需要听取网站的爬虫协议，有的可以爬，有的不能爬。在网站的域名后面加上robots.txt。如果出现404，可以随心所欲爬取。

user-agent：* 这个字段的意思是允许哪个引擎的爬虫获取数据，*代表所有类型的爬虫都可以

disallow：/admin/ 这个字段代表爬虫不允许爬那个路径下面的数据，如果是/的话，就代表所有路径下面的数据都不能爬

 

 
