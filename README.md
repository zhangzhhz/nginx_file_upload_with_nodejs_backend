# nginx_file_upload_with_nodejs_backend

#### **Claimer**:
The codes for nodejs server and clent side html/js come from https://javascript.info/resume-upload. I changed filePath and added some additional logging in this repository.

## What this repository contains
This repository contains an Nginx virutal host configuration, a nodejs server, and client side html/js for file uploading.
1. **nginx**:
   * **myserver**: This is the Nginx virtual host configuration. Usually this is in /etc/nginx/sites-enabaled/ on Ubuntu.
2. **nodejs**:
   * **server.js**: A nodejs server listening at port 8080. It handles writing uploaded content to files.
3. **html**: With configuration file `myserver`, these 2 files should be placed in the root directory of `myserver`.
   * **upload.html**: Sample web page for uplodaing files.
   * **uploader.js**: Client side javascript that use XMLHttpRequest for file uploading. Used by `upload.html`.

## Why I did this and what I tried

I set up a Nginx web server to serve my own Jupyter Notebook. Then I thought it would be a good idea to have the ability to upload files via Nginx.

I was not familiar with how uploading files to a web page worked, and how Nginx processed requests, so it took about a day or two's googling and trial-and-erorr for this.

1. There was a https://github.com/vkholodkov/nginx-upload-module/. But it seems that it requires re-compiling Nginx with this module. I skipped this.

2. I then found the following pages:
   * https://coderwall.com/p/swgfvw/nginx-direct-file-upload-without-passing-them-through-backend
   * https://stackoverflow.com/questions/44371643/nginx-php-failing-with-large-file-uploads-over-6-gb/44751210#44751210
   * https://github.com/ardinusawan/Nginx-direct-file-upload-without-passing-them-through-backend

   I skipped them because I didn't know a backend App server is needed for handling file contents uploaded and I went on searching for "pure" Nginx upload.

3. I found https://javascript.info/resume-upload. The codes run well with nodejs server alone. I tried including it with Nginx and failed because I didn't quite understand how Nginx processed requests at that time.

4. I then came back to the 3 pages in point 2 above. Basically they are the same and they use Nginx builtin parameter "client_body_in_file_only " to save files to disk and use other means to extract file content from there ("client_body_in_file_only" does not work with multipart/form-data, so "other means" is needed).

5. I finally tried point 3 again. I read some primer on Nginx processing, and came up with what I have now. It may not be efficient but works in my case.




