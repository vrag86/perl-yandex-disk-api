# NAME

**Yandex::Disk** - a simple API for Yandex Disk

# VERSION
 version 0.01

# METHODS

## getDiskInfo()

Return disk info data as hashref
    $disk->getDiskInfo();
Example output:
    {
        max\_file\_size    1073741824,
        revision         14987326771107,
        system\_folders   {
            applications    "disk:/Приложения",
            downloads       "disk:/Загрузки/",
            facebook        "disk:/Социальные сети/Facebook",
            google          "disk:/Социальные сети/Google+",
            instagram       "disk:/Социальные сети/Instagram",
            mailru          "disk:/Социальные сети/Мой Мир",
            odnoklassniki   "disk:/Социальные сети/Одноклассники",
            photostream     "disk:/Фотокамера/",
            screenshots     "disk:/Скриншоты/",
            social          "disk:/Социальные сети/",
            vkontakte       "disk:/Социальные сети/ВКонтакте"
        },
        total\_space      67645734912,
        trash\_size       0,
        used\_space       19942927435,
        user             {
            login   "login",
            uid     123456
        }
    }

## uploadFile(%opt)

Upload file (-file) to Yandex Disk in folder (-remote\_path). Return 1 if success
    $disk->uploadFile(-file => '/root/upload', -remote\_path => 'Temp', -overwrite => 0);
    Options:
        -overwrite          => Owervrite file if exists (default: 1)
        -remote\_path        => Path to upload file on disk
        -file               => Path to local file

## createFolder(%opt)

Create folder on disk
    $disk->createFolder(-path => 'Temp/test', -recursive => 1);
    Options:
        -path               => Path to folder,
        -recursive          => Recursive create folder (default: 0)

## deleteResource(%opt)

Delete file or folder from disk. Return 1 if success
    $disk->deleteResource(-path => 'Temp/test');
    Options:
        -path               => Path to delete file or folder
        -permanently        => Do not move to trash, delete permanently (default: 0)
        -wait               => Wait delete resource (defailt: 0)

## downloadFile(%opt)

Download file from Yandex Disk to local file. Method overwrites local file if exists. Return 1 if success
    $disk->downloadFile(-path => 'Temp/test', -file => 'test');
    Options:
        -path               => Path to file on Yandex Disk
        -file               => Path to local destination

## emptyTrash(%opt)

Empty trash. If -path specified, delete -path resource, otherwise - empty all trash. Return 1 if success
    $disk->emptyTrash(-path => 'Temp/test');        #Delete '/Temp/test' from trash
    Options:
        -path               => Path to resource on Yandex Disk to delete from trash
        -wait               => Wait empty trash (defailt: 0)

    $disk->emptyTrash;      #Full empty trash

## listFiles(%opt)

List files in folder. Return arrayref to hashref(keys: "path", "type", "name", "preview", "created", "modified", "md5", "mime\_type", "size")
    $disk->listFiles(-path => 'Temp/test');
    Options:
        -path               => Path to resource (file or folder) on Yandex Disk for which need get info
        -limit              => Limit max files to output (default: unlimited)
        -offset             => Offset records from start (default: 0)

# Public files

my $public = $disk->public();  #Create [Yandex::Disk::Public](https://metacpan.org/pod/Yandex::Disk::Public) object

# DEPENDENCE

[LWP::UserAgent](https://metacpan.org/pod/JSON::XS|URI::Escape|IO::Socket::SSL)

# AUTHORS

- Pavel Andryushin <vrag867@gmail.com>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2017 by Pavel Andryushin.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
