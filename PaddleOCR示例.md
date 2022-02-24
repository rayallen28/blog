# PaddleOCR示例
```python
from paddleocr import PaddleOCR
ocr = PaddleOCR(use_angle_cls=True, lang='ch')
result = ocr.ocr('page0.png', cls=True)
print(result)
```
