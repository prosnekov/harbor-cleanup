# harbor-cleanup
Automated script to delete tags from a [Harbor](https://github.com/vmware/harbor) registry

## Binaries
This fork was updated to work againt Harbor **1.9.X**

Authors:
- [Original repo](https://github.com/cavemandaveman/harbor-cleanup)
- [Used fork](https://github.com/clearent/harbor-cleanup)

## Building
*   Run `pip install -r requirements.txt`
*   Run `pyinstaller -F harbor-cleanup.py` to create `./dist/harbor-cleanup`

## Usage
```
usage: harbor-cleanup [-h] [-v] [-d] [-q] -i URL -u USER -p PASSWORD
                      [-c PRESERVE_COUNT]
                      project

Cleans up images in a Harbor project.

positional arguments:
  project               name of the Harbor project to clean

optional arguments:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
  -d, --debug           turn on debugging mode
  -q, --quiet           suppress console output
  -n, --dry-run         only print out image tags, do not do actual deletion
  -c PRESERVE_COUNT, --preserve-count PRESERVE_COUNT
                        keep the last n number of image tags (by reverse
                        alphanumerical order); defaults to 5
  -k FILE_PATH, --keep-file FILE_PATH
                        Keep the images mentioned in the file. The file should
                        contain one image & tag per record (project/image:tag)
  -pt TAG1              Global protected tags. Images with tags listed within 
                        this options will be kept in all repositories in defined project.
                        To protect multiple tags provide this key multiple times. Example: 
                        -pt develop -pt latest -pt stable

required arguments:
  -i URL, --url URL     URL of the Harbor instance
  -u USER, --user USER  valid Harbor user with proper access
  -p PASSWORD, --password PASSWORD
                        password for Harbor user
  ```

## Note
*   This tool shoud works against v1.X.X but have been tested only against 1.9.4 of Harbor
*   This will delete images, however the images will still take up disk space until you run [Garbage Collection](https://goharbor.io/docs/1.10/administration/garbage-collection/
