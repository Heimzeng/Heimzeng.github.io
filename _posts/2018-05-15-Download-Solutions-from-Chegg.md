---
layout: post
tags: spinner
title: "Download Solutions from Chegg"
---
Use selenium to dowmload solutions from chegg.

## 起因
有一天做作业遇到不会的题，然后试图Google一下答案，发现只有一个叫做[Chegg](http://www.chegg.com/)的网站上面有答案。

点击去有限制，需要一个VIP账号才能看所有的答案。

get了一个VIP账号，又发现所有的答案都是不可选中的模式，也就是不可以复制粘贴，更不可以下载，这大概是网站的版权保护吧。

而我要找的书有几百道题，可能在VIP到期前我都看不完这些答案，那怎么办呢？

一道道截图太麻烦了，所以我就想起之前做过的一个[抢票程序]()，使用的是selenium这个工具。

查了下selenium的用法，发现有一个对网页element截图的函数，开心，这么好用的工具当然要用起来。于是着手开发这个**自动截图Chegg答案工具**。

## 模拟登录

首先，我们运行一个Firefox浏览器并进入登录页面模拟登陆：

```python
    login_url = 'http://www.chegg.com/login'
    with open('user.txt', 'r') as userFile:
        username = userFile.readline().strip()
        password = userFile.readline().strip()
    b = Browser('firefox', headless=Ture)
    b.driver.maximize_window()
    b.driver.get(login_url)
    sleep(3)
    b.fill("email", username)
    b.fill("password", password)
    b.find_by_name(u"login").click()
    sleep(3)
```

其中的username和password从文件user.txt中读取并去除行尾的'\n', handless参数设置为True是为了让Firefox在后台运行，即不显示界面（好像这样子更高效？）。

我们将username和password分别填入"email"以及"password"这两个input element里面，并点击login button来实现登录操作。

**注意：以下所有操作都是在登录了VIP账号的前提下操作的。**

## 版本 1
起初为了尽快实现这个工具，而且刚开始没有发现一些书的答案是不齐全的，所以直接用了暴力遍历的方法。

这个方法简单而麻烦，简单是程序的实现上比较简单，但是需要人工去找出书中每个章节对应的problem的数量，然后手动写一个数组，like this：

```python
    P_num = 		[0, 53, 66, 81, 91, 85, 106, 69, 35, 49, 50, 45, 60, 53]
    M_num = 		[0, 10, 6, 	6, 	11, 6, 	21,  12, 14, 33, 12, 11, 12, 4 ]
```

解释一下，因为我将要下载的这本书的答案分为P类型的答案（problem）和M类型的答案（matlab），所以用两个数组分别表示每个章节这两种问题的数目。

接下来创建文件夹并利用URL的规律，直接暴力访问每个网站并且截图相应的element。

```python
    chapter_num = len(P_num)
    for chapter_i_1 in range(chapter_num):
        chapter_i = chapter_i_1 + 1
        P_DIR = './solution/chapter' + str(chapter_i) + '/P/'
        makeDirIfItsNotExist(P_DIR)
        M_DIR = './solution/chapter' + str(chapter_i) + '/M/'
        makeDirIfItsNotExist(M_DIR)
        elementId = 'solution-player-sdk'
        for pro_i_1 in range(P_num[chapter_i_1]):
            pro_i = pro_i_1 + 1
            screenshotFilename = str(pro_i) + 'P' + '.png'
            if not checkFileExist(P_DIR + screenshotFilename):
                print('P:', chapter_i, pro_i)
                url = 'http://www.chegg.com/homework-help/Digital-Signal-Processing-4th-edition-chapter-' + str(chapter_i) + '-problem-' + str(pro_i) + 'P-solution-9780073380490'
                getElementScreenshot(b.driver, url, elementId, 'id', P_DIR, screenshotFilename)
        for m_i_1 in range(M_num[chapter_i_1]):
            m_i = m_i_1 + 1
            screenshotFilename = str(m_i) + 'M' + '.png'
            if not checkFileExist(M_DIR + screenshotFilename):
                print('M:', chapter_i, m_i)
                url = 'http://www.chegg.com/homework-help/Digital-Signal-Processing-4th-edition-chapter-' + str(chapter_i) + '-problem-' + str(m_i) + 'M-solution-9780073380490'
                getElementScreenshot(b.driver, url, elementId, 'id', M_DIR, screenshotFilename)
```

其中getElementScreenshot函数如下：

```python
def getElementScreenshot(driver, url, elementIdentifier, idType, screenshotDir, screenshotFilename):
    driver.get(url)
    # 模拟滑动鼠标滚轮，加载所有的element
    scheight = .1
    while scheight < 10000:
        driver.execute_script("window.scrollTo(0, document.body.scrollHeight/%s);" % scheight)
        if scheight < 9.9:
            scheight += .01
        else:
             scheight += 10
    element = driver.find_element_by_id(elementIdentifier)       
    element.screenshot(screenshotDir + screenshotFilename)
```

整个程序只用了不到50行代码去实现，但是只能支持所有的章节的所有题目都有答案的情况，一旦有一个章节的答案不完整，比如说第一章的的第2题没有答案，那么答案列表便会是[1P, 3P, 4P, ...]这样子，那么程序就会推导出错的URL，进而不能得到相应的element，便会崩溃。

既然是崩溃的情况，有一个办法可以解决，那就是try。

我们在需要get到element的地方使用try，便能解决答案序号不连续的情况了：

```python
def getElementScreenshot(driver, url, elementIdentifier, idType, screenshotDir, screenshotFilename):
    ...
    try:
        element = driver.find_element_by_id(elementIdentifier)
    except Exception as e:
        print('cannot find element')
        print(e)
    else:
        pass
    finally:
        pass        
    element.screenshot(screenshotDir + screenshotFilename)
```

这样每次找不到答案的时候就只会报错而不会崩溃了，于是我们得到了所有答案。

[版本1链接](https://github.com/Heimzeng/SolutionDownloader/tree/v1.0)

## 版本 2
在版本1中还会存在一个问题，需要手动输入章节中所有问题的数目，虽然不是一个很耗时的操作，但是如果需要截图大量书籍的答案的话，那么也会是一个巨大的麻烦。所以就有了版本2。

其实解决这个问题也不难，思路大概就是找到管理chapter的那个总element，然后将里面的章节编号和问题编号全部存在数组里，然后按照版本1的方法遍历即可。

说起来很容易，做起来好像也不是那么难。就是需要复习下js。

直接上代码：

```python
    b.driver.get('http://www.chegg.com/homework-help/Digital-Signal-Processing-4th-edition-chapter-2-problem-1P-solution-9780073380490')
    jq_close_chapter_list = '$(".chapter.open h2").click()'
    b.driver.execute_script(jq_close_chapter_list)

    jq_get_chapters_name = 'var chapterNameArray = new Array();                                                     \
                            $(".chapters .chapter").each(function(index){                                           \
                                                             chapterNameArray.push($(this).text());                 \
                                                         });                                                        \
                            return chapterNameArray;                                                                \
                            '
    chapters_name = b.driver.execute_script(jq_get_chapters_name)

    jq_get_problems_names = 'var chapters = new Array();                                                            \
                            $(".chapters .chapter").each(function(index){                                           \
                                                            $(this).find("h2").click();                             \
                                                            var problemElementArray = new Array();                  \
                                                            $(this).find(".problems .problem").each(function(index){\
                                                                problemElementArray.push($(this).text());           \
                                                            });                                                     \
                                                            chapters.push(problemElementArray);                     \
                                                         });                                                        \
                            return chapters;                                                                        \
                            '
    problems_names = b.driver.execute_script(jq_get_problems_names)
```

由于我们在第一次打开一个作业答案的URL的时候，会有一个chapter的列表即当前列表是自动打开的，所以我们需要先关闭该章节，不然在后面读取章节编号的时候text里面会有问题的编号。

其实只要找到element对应的id/class/tag/name等信息，一切都变得简单。

得到编号后直接根据URL的规则遍历即可。

[版本2链接](https://github.com/Heimzeng/SolutionDownloader/tree/v2.0)

## 版本 3
在版本2中也存在一个小问题，那就是这个URL分解的问题，如果只输入一个URL、一个账号、一个密码就能得到一本书的答案，是不是想想都很舒服。

解决方案就是：没做。

## 后续
在我下载答案的后两天，chegg宣布整改：

<center>
	<img src="https://github.com/Heimzeng/Heimzeng.github.io/blob/master/assets/img/post/cheggDownloader/cheggDown.png?raw=true">
</center>

成就达成：入侵美国最大答案网站Chegg使其停业整改！