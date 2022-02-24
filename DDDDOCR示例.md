# DDDDOCR示例
```python
import ddddocr
ocr = ddddocr.DdddOcr()
with open('微信截图_20211028110801.png', 'rb') as f:
    image = f.read()
res = ocr.classification(image)
print(res)
```

