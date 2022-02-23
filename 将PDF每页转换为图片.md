# 将PDF每页转换为图片
```python
import fitz
# 将pdf中每页转换为图片
doc = fitz.open('a498db78-d63b-49f7-9463-611f2613881d.pdf')
zoom_x = 2.0
zoom_y = 2.0
mat = fitz.Matrix(zoom_x, zoom_y)
for page in doc:
    pix = page.get_pixmap(matrix=mat)
    pix.save('page %i.png' % page.number)
```
