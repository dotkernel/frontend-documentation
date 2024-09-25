# Clone the project

## Recommended development environment

> If you are using Windows as OS on your machine, you can use WSL2 as development environment.
> Read more here: [PHP-Mariadb-on-WLS2](https://www.dotkernel.com/php-development/almalinux-9-in-wsl2-install-php-apache-mariadb-composer-phpmyadmin/)

Using your terminal, navigate inside the directory you want to download the project files into.

> Make sure that
>
> - The directory is empty before proceeding to the download process.
>     - You will get this error if the directory is not empty `fatal: destination path '.' already exists and is not an empty directory.` and no files will be cloned.
> - That you have writing permissions on the directory.

Once there, run the following command:

```shell
git clone https://github.com/dotkernel/frontend.git .
```

If everything ran correctly, you can expect to see an output like this, though the numbers may differ.

```shell
Cloning into '.'...
remote: Enumerating objects: 6901, done.
remote: Counting objects: 100% (795/795), done.
remote: Compressing objects: 100% (343/343), done.
remote: Total 6901 (delta 522), reused 478 (delta 449), pack-reused 6106 (from 1)
Receiving objects: 100% (6901/6901), 3.83 MiB | 6.42 MiB/s, done.
Resolving deltas: 100% (3868/3868), done.
```

You can already open the project in your preferred IDE to double-check the files were copied correctly.
