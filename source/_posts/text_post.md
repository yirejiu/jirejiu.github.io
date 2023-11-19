---
title: 豆瓣影片排行榜
date: 2023-11-09 22:36:17
tags:
---
import requests
from bs4 import BeautifulSoup

for x in range(0,250,25):

    url = f"https://movie.douban.com/top250?start={x}"

    headers = {
              "User-Agent":"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36 Edg/119.0.0.0"
    }

    response = requests.get(url, headers=headers)
    content = response.content.decode('utf8')
    soup = BeautifulSoup(content, "lxml")
    ranks = soup.findAll('span', attrs={"class": "title"})
    for rank in ranks:
        rank_string = rank.string
        if "/" not in rank_string:
            print(rank_string)
