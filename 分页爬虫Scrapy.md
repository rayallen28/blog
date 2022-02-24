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

爬虫结果解析：

```perl
#!perl
use utf8;
use v5.24;
use strict;
use Cwd;
use Encode qw/ encode decode/;

open WEB_LOG, '<:encoding(UTF-8)', 'log.txt' or die;
open NEW_LOG, '>:encoding(UTF-8)', 'new_log.txt' or die;
foreach(<WEB_LOG>){
	chomp;
	s/\A公司//;
	s/\A银行//;
	s/公开\z//;
	s/公告\z//;
	s/\s//;
	if(/体检|广告|安保|保安|食材|用房|驾驶|委外|宣传|印刷|保险|车辆|律师|食堂|汽车|零星|
		换行|会议|楼顶|收费|押钞|封闭|灯光|贴息|开水|变电|布线|工程审计|快递/){
		next;
	}
	say NEW_LOG $_;
}
close WEB_LOG;
close NEW_LOG;
```
