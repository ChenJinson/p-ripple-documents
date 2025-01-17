---
title: file - File
description: PRipple supports operating files through the \P\IO::File() method, which is used to handle file read and write operations.
keywords: ['PRipple', 'PHP', 'coroutine', 'high performance', 'high concurrency', 'file', 'IO']
---

> ⚠️ This page was initialized by AI translation and may contain outdated or inaccurate information. If there are
> inaccuracies, please submit changes to correct these errors [Correct](https://github.com/cloudtay/p-ripple-documents)

### Access components

```php
\P\IO::File() : File;
```

###API

```php
public function getContents(string $path): Promise;
public function open(string $path, string $mode): Stream;
```

### Overview

PRipple provides asynchronous operation methods for files, allowing developers to read file contents and operate file
streams through streams that do not block the process.

### Instructions

You can read the file in the following way

```php
\P\IO::File()->getContents(__FILE__)->then(function(string $value){
    
});
```

```php
\P\async(function(){
    $value = \P\await(
        \P\IO::File()->getContents(__FILE__)
    );
});
```

You can also open a file stream in the following way

```php
$stream = \P\IO::File()->open('file.txt','r');
```

Stream follows the StreamInterface development of PSR specifications. For Stream operations, please see the Stream
operation section.
