# Down the Wormhole
```bash
steghide -p diggingdeeper -sf wormhole.jpg
```
#next.txt
After diving through the wormhole, you find yourself in front of a rabbit hole. What secrets lie inside?

https://niccgetsspooky.xyz/r/a/b/b/i/t/h/o/l/e/rabbit-hole.svg

# on the website there is a huge base64/32 string
![grafik](https://github.com/MoaathOudeh/spookyCTF/assets/127448426/421868ec-139c-48b5-af42-a44797118f58)

this is basically zip files (in a look, hence wormhole)

# solve script

```py
import os
import subprocess

def extract_with_atool(filename):
    try:
        print(f"Extracting {filename}")
        subprocess.run(['atool', '-x', filename])
        return True
    except Exception as e:
        print(f"Error extracting {filename}: {str(e)}")
        return False

def recursively_extract_nested_archives(filename):
    while True:
        if not extract_with_atool(filename):
            break
        os.remove(filename)
        new_archive = os.popen('ls secrets*').read().strip()
        if filename == new_archive:
            break
        filename = new_archive

if __name__ == "__main__":
    initial_file = "secrets665.zip.bz2.gz"

    recursively_extract_nested_archives(initial_file)
```
flag: NICC{TH3-UF0S-4R3-UP-N0T-D0WN-50-WHY-4R3-Y0U-D0WN-H3R3}

