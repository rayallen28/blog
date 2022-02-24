# CNOCR示例
```python
from cnocr import CnOcr
from cnstd import CnStd
ocr = CnOcr()
std = CnStd()
box_info_list = std.detect('page0.png')
for box_info in box_info_list['detected_texts']:
    cropped_img = box_info['cropped_img']
    ocr_res = ocr.ocr_for_single_line(cropped_img)
    print(f'ocr result: {ocr_res}')
```
要搭配cnstd，先检测文本，再识别文本
