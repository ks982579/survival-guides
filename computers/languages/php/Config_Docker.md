This [stackOverflow](https://stackoverflow.com/questions/48525092/docker-httpd-configuration-error-no-mpm-loaded) post talks about overcoming a "No MPM Loaded" error at the end of creating the docker file and running the image. 

> Just add `LoadModule mpm_event_module modules/mod_mpm_event.so` into `httpd.conf` above the other LoadModule directives.

That's not the issue. This appears to be the issue, from [gitHub.com](https://github.com/docker-library/httpd/issues/157), which links to this [stackOverflow](https://stackoverflow.com/questions/60741614/ah00534-httpd-configuration-error-no-mpm-loaded-when-copying-my-own-httpd-co) page. Basically, you have to open in Notepad, and re-save-as, changing the "Encoding" dropdown at the very bottom of the "save-as" window. 