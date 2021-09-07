# Gang Busted

![Gang Busted description](./assets/gang_busted_description.png "Gang Busted")

Once I've downloaded and unzipped the archive, the main directory extracted was "data" and inside that I found this:

![Directories](./assets/directories.png)

When I listed the directory, I found that it was some acquired Android data.
Most of these directories were empty. To clean this, I ran the following command inside the "data" directory:

```bash
$ find . -empty -type d -delete
``` 
**This is a key point:** In Android filesystem, every application stores its data under the **/data/data** folder. Furthermore, Android uses SQLite to store most data (emails, text messages, etc).


