zip linux ubuntu

# Zip
[learn zip](https://learnubuntu.com/zip-folder/)


```bash
zip <ouput-file> <inputfile>
```

- `.` to inlucde everythign in current directory

```bash
zip output.zip .
```

- `-r` to save directory structure

- `-x` to not include certain files, use `"folder/*"` for folder names otherwise it will include the content of the folder and exclude only the main folder itself
```bash
zip output.zip . -x .env "node-modules"
```