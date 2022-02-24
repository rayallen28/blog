# 分页爬虫Scrapy
```python
# -*- coding:utf-8 -*-
import scrapy
from urllib.parse import urljoin

class ExampleSpider(scrapy.Spider):
    name = 'example'
    allowed_domains = ['iframe.***.com.cn']
    start_urls = ['http://iframe.***.com.cn/html1/category/181313/7338-1.htm']

    page_url = None

    def parse(self, response):
        titles = response.xpath('////*[@id="ReportIDname"]/a/@title').extract()
        f = open('d://log.txt', 'a', encoding='gbk')
        for title in titles:
            f.write(title.strip() + '\n')
        f.close()
        #下一页
        self.page_url = response.xpath('//*[@id="CBNext"]/@href').extract()

        for next_url in self.page_url:
            yield scrapy.Request(urljoin('http://iframe.***.com.cn', next_url), callback=self.parse)
```
定义起始页面

找到下一页的xpath

走到下一页

