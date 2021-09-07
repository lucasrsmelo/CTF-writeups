# Gang Busted
<p align="center">
![gang_busted_description](https://user-images.githubusercontent.com/34749742/132276116-3c033395-d87e-4bca-aa04-abc244ab25a6.png)
</p>
Once I've downloaded and unzipped the archive, the main directory extracted was "data" and inside that I found this:

![Directories](https://user-images.githubusercontent.com/34749742/132276082-cb7f6e25-dab4-4b7a-9b2a-fd8e2d1bb00b.png)

When I listed the directory, I found that it was some acquired Android data.
Most of these directories were empty. To clean this, I ran the following command inside the "data" directory:

```bash
$ find . -empty -type d -delete
``` 
**This is a key point:** In Android filesystem, every application stores its data under the **/data/data** folder. Furthermore, Android uses SQLite to store most data (emails, text messages, etc).


