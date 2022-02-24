# Windows录音文件（m4a）转wav
```python
def m4a_to_wav(m4a_file, wav_file):
    """Convert an m4a file to a wav file"""
    import os
    import subprocess
    command = "ffmpeg -i {} -ac 1 -ar 16000 {}".format(m4a_file, wav_file)
    subprocess.call(command, shell=True)
    os.remove(m4a_file)
m4a_to_wav("d://py//录音.m4a", "d://py//录音.wav")
```
需要安装ffmpeg
