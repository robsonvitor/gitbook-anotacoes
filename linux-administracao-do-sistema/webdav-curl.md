# webdav - CURL



Assuming the following Data:

* **Webdav URL:** http://example.com/webdav
* **Username:** user
* **Password:** pass

### Actions

#### Reading Files/Folders

| 1 | `curl` `'`[`http://example.com/webdav`](http://example.com/webdav)`'` |
| :--- | :--- |


#### Creating new Folder

| 1 | `curl -X MKCOL` `'`[`http://example.com/webdav/new_folder`](http://example.com/webdav/new_folder)`'` |
| :--- | :--- |


#### Uploading File

| 1 | `curl -T` `'/path/to/local/file.txt'` `'`[`http://example.com/webdav/test/new_name.txt`](http://example.com/webdav/test/new_name.txt)`'` |
| :--- | :--- |


#### Renaming File

| 1 | `curl -X MOVE --header` `'Destination:`[`http://example.org/webdav/new.txt`](http://example.org/webdav/new.txt)`'` `'`[`http://example.com/webdav/old.txt`](http://example.com/webdav/old.txt)`'` |
| :--- | :--- |


#### Deleting Files/Folders

**File:**

| 1 | `curl -X DELETE` `'`[`http://example.com/webdav/test.txt`](http://example.com/webdav/test.txt)`'` |
| :--- | :--- |


**Folder:**

| 1 | `curl -X DELETE` `'`[`http://example.com/webdav/test`](http://example.com/webdav/test)`'` |
| :--- | :--- |


#### List Files in a Folder

| 123456 | `curl -i -X PROPFIND http://example.com/webdav/` `--upload-file` `- -H` `"Depth: 1"` `<<end<?xml version="1.0"?><a:propfind xmlns:a="DAV:"><a:prop><a:resourcetype/></a:prop></a:propfind>end` |
| :--- | :--- |


### Options

#### Authentication

**Basic:**

| 1 | `curl --basic --user` `'user:pass'` `'`[`http://example.com/webdav`](http://example.com/webdav)`'` |
| :--- | :--- |


**Digest:**

| 1 | `curl --digest --user` `'user:pass'` `'`[`http://example.com/webdav`](http://example.com/webdav)`'` |
| :--- | :--- |


**let cURL choose:**

| 1 | `curl --anyauth --user` `'user:pass'` `'`[`http://example.com/webdav`](http://example.com/webdav)`'` |
| :--- | :--- |


#### Get response code

| 1 | `curl -X DELETE` `'`[`http://example.com/webdav/test`](http://example.com/webdav/test)`'` `-sw` `'%{http_code}'` |
| :--- | :--- |


Fonte: [https://code.blogs.iiidefix.net/posts/webdav-with-curl/](https://code.blogs.iiidefix.net/posts/webdav-with-curl/)

