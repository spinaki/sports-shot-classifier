1. Start Notebook
2. Get Token for Notebook: Run `jupyter notebook list`
```bash
Currently running servers:
http://0.0.0.0:8888/?token=db8fc868ed3f92ff3e354449c8b15a05c1b6482e61d3bced :: /notebooks
```
3. Copy the token.
4. Get the file urls from paperspace by going to the `/storage` directory. Use that to create the base_url below.
5. Replace the `view` in the above url with `files`
6. Create a list of files in each classes / subdirectories and download them as text files.
7. Run the code below.

```bash
import urllib.request

def chomp(x):
    if x.endswith("\r\n"): return x[:-2]
    if x.endswith("\n") or x.endswith("\r"): return x[:-1]
    return x

base_dir = "/home/download/tennis"
base_url="https://nkiwcabw.gradient.paperspace.com/files/storage/data/pinaki/tennis/"
token = "c52314bb3bb744d7835690c614bbe6a6412f4e44a8934ca2"
classes = ["serve", "forehand", "backhand", "smash"]
for c in classes:
    # url = base_url + c + ".txt"+ "?token=" + token
    class_dir =  base_dir + c + "/"
    class_file = base_dir + c + ".txt"
    # print(url)
    # urllib.request.urlretrieve(url, base_dir + c + ".txt")
    with open(class_file) as f:
        print(class_file)
        my_list = list(f)
        my_list = [ chomp(s) for s in my_list]
        print(len(my_list))
        i = 0
        for f in my_list:
            img_file = class_dir + f
            img_url = base_url + c + "/" + f + "?token=" + token
            urllib.request.urlretrieve(img_url, img_file)
            i = i + 1
            if i % 10 == 0:
                print(i)
            # print(img_file)
            # print(img_url)
            # break
        break
```