---
title: pip3 install scrapy
categories:
  - Python
tags:
  - python3
  - scrapy
  - python
abbrlink: 10113
date: 2019-08-31 14:52:08
---


##  l@192  ~  python3 -m pip install --upgrade pip
 

```
WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ReadTimeoutError("HTTPSConnectionPool(host='pypi.org', port=443): Read timed out. (read timeout=15)")': /simple/pip/
WARNING: Retrying (Retry(total=3, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ReadTimeoutError("HTTPSConnectionPool(host='pypi.org', port=443): Read timed out. (read timeout=15)")': /simple/pip/
WARNING: Retrying (Retry(total=2, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ReadTimeoutError("HTTPSConnectionPool(host='pypi.org', port=443): Read timed out. (read timeout=15)")': /simple/pip/
WARNING: Retrying (Retry(total=1, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ReadTimeoutError("HTTPSConnectionPool(host='pypi.org', port=443): Read timed out. (read timeout=15)")': /simple/pip/
WARNING: Retrying (Retry(total=0, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ReadTimeoutError("HTTPSConnectionPool(host='pypi.org', port=443): Read timed out. (read timeout=15)")': /simple/pip/
Requirement already up-to-date: pip in /usr/local/lib/python3.7/site-packages (19.1.1)
```

##  l@192  ~  pip3 install scrapy
 
 ```
Collecting scrapy
  Downloading https://files.pythonhosted.org/packages/29/4b/585e8e111ffb01466c59281f34febb13ad1a95d7fb3919fd57c33fc732a5/Scrapy-1.7.3-py2.py3-none-any.whl (234kB)
     |████████▍                       | 61kB 11kB/s eta 0:00:15ERROR: Exception:
Traceback (most recent call last):
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/urllib3/response.py", line 360, in _error_catcher
    yield
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/urllib3/response.py", line 442, in read
    data = self._fp.read(amt)
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/cachecontrol/filewrapper.py", line 62, in read
    data = self.__fp.read(amt)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/http/client.py", line 457, in read
    n = self.readinto(b)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/http/client.py", line 501, in readinto
    n = self.fp.readinto(b)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/socket.py", line 589, in readinto
    return self._sock.recv_into(b)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/ssl.py", line 1071, in recv_into
    return self.read(nbytes, buffer)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/ssl.py", line 929, in read
    return self._sslobj.read(len, buffer)
socket.timeout: The read operation timed out

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/cli/base_command.py", line 178, in main
    status = self.run(options, args)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/commands/install.py", line 352, in run
    resolver.resolve(requirement_set)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/resolve.py", line 131, in resolve
    self._resolve_one(requirement_set, req)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/resolve.py", line 294, in _resolve_one
    abstract_dist = self._get_abstract_dist_for(req_to_install)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/resolve.py", line 242, in _get_abstract_dist_for
    self.require_hashes
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/operations/prepare.py", line 347, in prepare_linked_requirement
    progress_bar=self.progress_bar
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 886, in unpack_url
    progress_bar=progress_bar
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 746, in unpack_http_url
    progress_bar)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 954, in _download_http_url
    _download_url(resp, link, content_file, hashes, progress_bar)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 683, in _download_url
    hashes.check_against_chunks(downloaded_chunks)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/utils/hashes.py", line 62, in check_against_chunks
    for chunk in chunks:
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 651, in written_chunks
    for chunk in chunks:
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/utils/ui.py", line 156, in iter
    for x in it:
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 640, in resp_read
    decode_content=False):
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/urllib3/response.py", line 494, in stream
    data = self.read(amt=amt, decode_content=decode_content)
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/urllib3/response.py", line 459, in read
    raise IncompleteRead(self._fp_bytes_read, self.length_remaining)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/contextlib.py", line 130, in __exit__
    self.gen.throw(type, value, traceback)
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/urllib3/response.py", line 365, in _error_catcher
    raise ReadTimeoutError(self._pool, None, 'Read timed out.')
pip._vendor.urllib3.exceptions.ReadTimeoutError: HTTPSConnectionPool(host='files.pythonhosted.org', port=443): Read timed out.
```

## ** ✘ l@192  ~  pip3 install scrapy


```
Collecting scrapy
  WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ReadTimeoutError("HTTPSConnectionPool(host='pypi.org', port=443): Read timed out. (read timeout=15)")': /simple/scrapy/
  WARNING: Retrying (Retry(total=3, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ReadTimeoutError("HTTPSConnectionPool(host='pypi.org', port=443): Read timed out. (read timeout=15)")': /simple/scrapy/
  Downloading https://files.pythonhosted.org/packages/29/4b/585e8e111ffb01466c59281f34febb13ad1a95d7fb3919fd57c33fc732a5/Scrapy-1.7.3-py2.py3-none-any.whl (234kB)
ERROR: Exception:
Traceback (most recent call last):
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/urllib3/response.py", line 360, in _error_catcher
    yield
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/urllib3/response.py", line 442, in read
    data = self._fp.read(amt)
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/cachecontrol/filewrapper.py", line 62, in read
    data = self.__fp.read(amt)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/http/client.py", line 457, in read
    n = self.readinto(b)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/http/client.py", line 501, in readinto
    n = self.fp.readinto(b)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/socket.py", line 589, in readinto
    return self._sock.recv_into(b)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/ssl.py", line 1071, in recv_into
    return self.read(nbytes, buffer)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/ssl.py", line 929, in read
    return self._sslobj.read(len, buffer)
socket.timeout: The read operation timed out

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/cli/base_command.py", line 178, in main
    status = self.run(options, args)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/commands/install.py", line 352, in run
    resolver.resolve(requirement_set)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/resolve.py", line 131, in resolve
    self._resolve_one(requirement_set, req)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/resolve.py", line 294, in _resolve_one
    abstract_dist = self._get_abstract_dist_for(req_to_install)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/resolve.py", line 242, in _get_abstract_dist_for
    self.require_hashes
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/operations/prepare.py", line 347, in prepare_linked_requirement
    progress_bar=self.progress_bar
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 886, in unpack_url
    progress_bar=progress_bar
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 746, in unpack_http_url
    progress_bar)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 954, in _download_http_url
    _download_url(resp, link, content_file, hashes, progress_bar)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 683, in _download_url
    hashes.check_against_chunks(downloaded_chunks)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/utils/hashes.py", line 62, in check_against_chunks
    for chunk in chunks:
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 651, in written_chunks
    for chunk in chunks:
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/utils/ui.py", line 156, in iter
    for x in it:
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 640, in resp_read
    decode_content=False):
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/urllib3/response.py", line 494, in stream
    data = self.read(amt=amt, decode_content=decode_content)
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/urllib3/response.py", line 459, in read
    raise IncompleteRead(self._fp_bytes_read, self.length_remaining)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/contextlib.py", line 130, in __exit__
    self.gen.throw(type, value, traceback)
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/urllib3/response.py", line 365, in _error_catcher
    raise ReadTimeoutError(self._pool, None, 'Read timed out.')
pip._vendor.urllib3.exceptions.ReadTimeoutError: HTTPSConnectionPool(host='files.pythonhosted.org', port=443): Read timed out.
 ✘ l@192  ~  sudo pip3 install lxml
Password:
WARNING: The directory '/Users/l/Library/Caches/pip/http' or its parent directory is not owned by the current user and the cache has been disabled. Please check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.
WARNING: The directory '/Users/l/Library/Caches/pip' or its parent directory is not owned by the current user and caching wheels has been disabled. check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.
Collecting lxml
  ERROR: Could not find a version that satisfies the requirement lxml (from versions: none)
ERROR: No matching distribution found for lxml
```


##  ✘ l@192  ~  pip3 install Scrapy


```
Collecting Scrapy
  WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ReadTimeoutError("HTTPSConnectionPool(host='files.pythonhosted.org', port=443): Read timed out. (read timeout=15)")': /packages/29/4b/585e8e111ffb01466c59281f34febb13ad1a95d7fb3919fd57c33fc732a5/Scrapy-1.7.3-py2.py3-none-any.whl
  Downloading https://files.pythonhosted.org/packages/29/4b/585e8e111ffb01466c59281f34febb13ad1a95d7fb3919fd57c33fc732a5/Scrapy-1.7.3-py2.py3-none-any.whl (234kB)
     |████████████████████████████████| 235kB 83kB/s
Collecting pyOpenSSL (from Scrapy)
  ERROR: Could not find a version that satisfies the requirement pyOpenSSL (from Scrapy) (from versions: none)
ERROR: No matching distribution found for pyOpenSSL (from Scrapy)
```


##  ✘ l@192  ~  pip3 install Scrapy


```
Collecting Scrapy
  Using cached https://files.pythonhosted.org/packages/29/4b/585e8e111ffb01466c59281f34febb13ad1a95d7fb3919fd57c33fc732a5/Scrapy-1.7.3-py2.py3-none-any.whl
Collecting parsel>=1.5 (from Scrapy)
  Downloading https://files.pythonhosted.org/packages/86/c8/fc5a2f9376066905dfcca334da2a25842aedfda142c0424722e7c497798b/parsel-1.5.2-py2.py3-none-any.whl
Collecting w3lib>=1.17.0 (from Scrapy)
  Downloading https://files.pythonhosted.org/packages/6a/45/1ba17c50a0bb16bd950c9c2b92ec60d40c8ebda9f3371ae4230c437120b6/w3lib-1.21.0-py2.py3-none-any.whl
Collecting pyOpenSSL (from Scrapy)
  WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ReadTimeoutError("HTTPSConnectionPool(host='pypi.org', port=443): Read timed out. (read timeout=15)")': /simple/pyopenssl/
  WARNING: Retrying (Retry(total=3, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ReadTimeoutError("HTTPSConnectionPool(host='pypi.org', port=443): Read timed out. (read timeout=15)")': /simple/pyopenssl/
  Downloading https://files.pythonhosted.org/packages/01/c8/ceb170d81bd3941cbeb9940fc6cc2ef2ca4288d0ca8929ea4db5905d904d/pyOpenSSL-19.0.0-py2.py3-none-any.whl (53kB)
     |████████████████████████▋       | 40kB 1.8kB/s eta 0:00:08ERROR: Exception:
Traceback (most recent call last):
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/urllib3/response.py", line 360, in _error_catcher
    yield
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/urllib3/response.py", line 442, in read
    data = self._fp.read(amt)
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/cachecontrol/filewrapper.py", line 62, in read
    data = self.__fp.read(amt)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/http/client.py", line 457, in read
    n = self.readinto(b)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/http/client.py", line 501, in readinto
    n = self.fp.readinto(b)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/socket.py", line 589, in readinto
    return self._sock.recv_into(b)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/ssl.py", line 1071, in recv_into
    return self.read(nbytes, buffer)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/ssl.py", line 929, in read
    return self._sslobj.read(len, buffer)
socket.timeout: The read operation timed out

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/cli/base_command.py", line 178, in main
    status = self.run(options, args)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/commands/install.py", line 352, in run
    resolver.resolve(requirement_set)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/resolve.py", line 131, in resolve
    self._resolve_one(requirement_set, req)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/resolve.py", line 294, in _resolve_one
    abstract_dist = self._get_abstract_dist_for(req_to_install)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/resolve.py", line 242, in _get_abstract_dist_for
    self.require_hashes
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/operations/prepare.py", line 347, in prepare_linked_requirement
    progress_bar=self.progress_bar
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 886, in unpack_url
    progress_bar=progress_bar
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 746, in unpack_http_url
    progress_bar)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 954, in _download_http_url
    _download_url(resp, link, content_file, hashes, progress_bar)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 683, in _download_url
    hashes.check_against_chunks(downloaded_chunks)
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/utils/hashes.py", line 62, in check_against_chunks
    for chunk in chunks:
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 651, in written_chunks
    for chunk in chunks:
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/utils/ui.py", line 156, in iter
    for x in it:
  File "/usr/local/lib/python3.7/site-packages/pip/_internal/download.py", line 640, in resp_read
    decode_content=False):
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/urllib3/response.py", line 494, in stream
    data = self.read(amt=amt, decode_content=decode_content)
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/urllib3/response.py", line 459, in read
    raise IncompleteRead(self._fp_bytes_read, self.length_remaining)
  File "/usr/local/Cellar/python/3.7.4/Frameworks/Python.framework/Versions/3.7/lib/python3.7/contextlib.py", line 130, in __exit__
    self.gen.throw(type, value, traceback)
  File "/usr/local/lib/python3.7/site-packages/pip/_vendor/urllib3/response.py", line 365, in _error_catcher
    raise ReadTimeoutError(self._pool, None, 'Read timed out.')
pip._vendor.urllib3.exceptions.ReadTimeoutError: HTTPSConnectionPool(host='files.pythonhosted.org', port=443): Read timed out.
```

##  ✘ l@192  ~  sudo pip3 install --upgrade pyopenssl


```
Password:
WARNING: The directory '/Users/l/Library/Caches/pip/http' or its parent directory is not owned by the current user and the cache has been disabled. Please check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.
WARNING: The directory '/Users/l/Library/Caches/pip' or its parent directory is not owned by the current user and caching wheels has been disabled. check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.
Collecting pyopenssl
  Downloading https://files.pythonhosted.org/packages/01/c8/ceb170d81bd3941cbeb9940fc6cc2ef2ca4288d0ca8929ea4db5905d904d/pyOpenSSL-19.0.0-py2.py3-none-any.whl (53kB)
     |████████████████████████████████| 61kB 27kB/s
Collecting cryptography>=2.3 (from pyopenssl)
  Downloading https://files.pythonhosted.org/packages/63/4e/57b7a6bd98906872fcd2531e74b532de2abe17d675a5cf171931fcb4a9e8/cryptography-2.7-cp34-abi3-macosx_10_6_intel.whl (1.6MB)
     |████████████████████████████████| 1.6MB 3.7MB/s
Collecting six>=1.5.2 (from pyopenssl)
  Downloading https://files.pythonhosted.org/packages/73/fb/00a976f728d0d1fecfe898238ce23f502a721c0ac0ecfedb80e0d88c64e9/six-1.12.0-py2.py3-none-any.whl
Collecting asn1crypto>=0.21.0 (from cryptography>=2.3->pyopenssl)
  Downloading https://files.pythonhosted.org/packages/ea/cd/35485615f45f30a510576f1a56d1e0a7ad7bd8ab5ed7cdc600ef7cd06222/asn1crypto-0.24.0-py2.py3-none-any.whl (101kB)
     |████████████████████████████████| 102kB 7.0MB/s
Collecting cffi!=1.11.3,>=1.8 (from cryptography>=2.3->pyopenssl)
  Downloading https://files.pythonhosted.org/packages/f0/48/5aa4ea664eba26dd5142558d04762f5065c02220b4665b3f7eecb9bb614e/cffi-1.12.3-cp37-cp37m-macosx_10_9_x86_64.whl (169kB)
     |████████████████████████████████| 174kB 6.6MB/s
Collecting pycparser (from cffi!=1.11.3,>=1.8->cryptography>=2.3->pyopenssl)
  Downloading https://files.pythonhosted.org/packages/68/9e/49196946aee219aead1290e00d1e7fdeab8567783e83e1b9ab5585e6206a/pycparser-2.19.tar.gz (158kB)
     |████████████████████████████████| 163kB 14.7MB/s
Building wheels for collected packages: pycparser
  Building wheel for pycparser (setup.py) ... done
  Stored in directory: /Users/l/Library/Caches/pip/wheels/f2/9a/90/de94f8556265ddc9d9c8b271b0f63e57b26fb1d67a45564511
Successfully built pycparser
Installing collected packages: six, asn1crypto, pycparser, cffi, cryptography, pyopenssl
Successfully installed asn1crypto-0.24.0 cffi-1.12.3 cryptography-2.7 pycparser-2.19 pyopenssl-19.0.0 six-1.12.0
```
##  l@192  ~  sudo pip3 install scrapy

```
WARNING: The directory '/Users/l/Library/Caches/pip/http' or its parent directory is not owned by the current user and the cache has been disabled. Please check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.
WARNING: The directory '/Users/l/Library/Caches/pip' or its parent directory is not owned by the current user and caching wheels has been disabled. check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.
Collecting scrapy
  Downloading https://files.pythonhosted.org/packages/29/4b/585e8e111ffb01466c59281f34febb13ad1a95d7fb3919fd57c33fc732a5/Scrapy-1.7.3-py2.py3-none-any.whl (234kB)
     |████████████████████████████████| 235kB 4.4kB/s
Collecting w3lib>=1.17.0 (from scrapy)
  Downloading https://files.pythonhosted.org/packages/6a/45/1ba17c50a0bb16bd950c9c2b92ec60d40c8ebda9f3371ae4230c437120b6/w3lib-1.21.0-py2.py3-none-any.whl
Collecting lxml; python_version != "3.4" (from scrapy)
  Downloading https://files.pythonhosted.org/packages/bd/9f/6cda4672d3ad1aa4cf818ab8401a763787efba751c88aaf4b38fc8f923bb/lxml-4.4.1-cp37-cp37m-macosx_10_6_intel.macosx_10_9_intel.macosx_10_9_x86_64.macosx_10_10_intel.macosx_10_10_x86_64.whl (8.9MB)
     |████████████████████████████████| 8.9MB 97kB/s
Collecting Twisted>=13.1.0; python_version != "3.4" (from scrapy)
  Downloading https://files.pythonhosted.org/packages/61/31/3855dcacd1d3b2e60c0b4ccc8e727b8cd497bd7087d327d81a9f0cbb580c/Twisted-19.7.0.tar.bz2 (3.1MB)
     |████████████████████████████████| 3.1MB 207kB/s
Collecting parsel>=1.5 (from scrapy)
  Downloading https://files.pythonhosted.org/packages/86/c8/fc5a2f9376066905dfcca334da2a25842aedfda142c0424722e7c497798b/parsel-1.5.2-py2.py3-none-any.whl
Requirement already satisfied: pyOpenSSL in /usr/local/lib/python3.7/site-packages (from scrapy) (19.0.0)
Requirement already satisfied: six>=1.5.2 in /usr/local/lib/python3.7/site-packages (from scrapy) (1.12.0)
Collecting queuelib (from scrapy)
  Downloading https://files.pythonhosted.org/packages/4c/85/ae64e9145f39dd6d14f8af3fa809a270ef3729f3b90b3c0cf5aa242ab0d4/queuelib-1.5.0-py2.py3-none-any.whl
Collecting cssselect>=0.9 (from scrapy)
  Downloading https://files.pythonhosted.org/packages/3b/d4/3b5c17f00cce85b9a1e6f91096e1cc8e8ede2e1be8e96b87ce1ed09e92c5/cssselect-1.1.0-py2.py3-none-any.whl
Collecting service-identity (from scrapy)
  Downloading https://files.pythonhosted.org/packages/e9/7c/2195b890023e098f9618d43ebc337d83c8b38d414326685339eb024db2f6/service_identity-18.1.0-py2.py3-none-any.whl
Collecting PyDispatcher>=2.0.5 (from scrapy)
  Downloading https://files.pythonhosted.org/packages/cd/37/39aca520918ce1935bea9c356bcbb7ed7e52ad4e31bff9b943dfc8e7115b/PyDispatcher-2.0.5.tar.gz
Collecting zope.interface>=4.4.2 (from Twisted>=13.1.0; python_version != "3.4"->scrapy)
  Downloading https://files.pythonhosted.org/packages/d9/3a/101934e0f2026f0a58698978bfedec6e2021b28b846d9e1d9b54369e044d/zope.interface-4.6.0-cp37-cp37m-macosx_10_14_x86_64.whl (131kB)
     |████████████████████████████████| 133kB 124kB/s
Collecting constantly>=15.1 (from Twisted>=13.1.0; python_version != "3.4"->scrapy)
  Downloading https://files.pythonhosted.org/packages/b9/65/48c1909d0c0aeae6c10213340ce682db01b48ea900a7d9fce7a7910ff318/constantly-15.1.0-py2.py3-none-any.whl
Collecting incremental>=16.10.1 (from Twisted>=13.1.0; python_version != "3.4"->scrapy)
  Downloading https://files.pythonhosted.org/packages/f5/1d/c98a587dc06e107115cf4a58b49de20b19222c83d75335a192052af4c4b7/incremental-17.5.0-py2.py3-none-any.whl
Collecting Automat>=0.3.0 (from Twisted>=13.1.0; python_version != "3.4"->scrapy)
  Downloading https://files.pythonhosted.org/packages/a3/86/14c16bb98a5a3542ed8fed5d74fb064a902de3bdd98d6584b34553353c45/Automat-0.7.0-py2.py3-none-any.whl
Collecting hyperlink>=17.1.1 (from Twisted>=13.1.0; python_version != "3.4"->scrapy)
  Downloading https://files.pythonhosted.org/packages/7f/91/e916ca10a2de1cb7101a9b24da546fb90ee14629e23160086cf3361c4fb8/hyperlink-19.0.0-py2.py3-none-any.whl
Collecting PyHamcrest>=1.9.0 (from Twisted>=13.1.0; python_version != "3.4"->scrapy)
  Downloading https://files.pythonhosted.org/packages/9a/d5/d37fd731b7d0e91afcc84577edeccf4638b4f9b82f5ffe2f8b62e2ddc609/PyHamcrest-1.9.0-py2.py3-none-any.whl (52kB)
     |████████████████████████████████| 61kB 123kB/s
Collecting attrs>=17.4.0 (from Twisted>=13.1.0; python_version != "3.4"->scrapy)
  Downloading https://files.pythonhosted.org/packages/23/96/d828354fa2dbdf216eaa7b7de0db692f12c234f7ef888cc14980ef40d1d2/attrs-19.1.0-py2.py3-none-any.whl
Requirement already satisfied: cryptography>=2.3 in /usr/local/lib/python3.7/site-packages (from pyOpenSSL->scrapy) (2.7)
Collecting pyasn1 (from service-identity->scrapy)
  Downloading https://files.pythonhosted.org/packages/6a/6e/209351ec34b7d7807342e2bb6ff8a96eef1fd5dcac13bdbadf065c2bb55c/pyasn1-0.4.6-py2.py3-none-any.whl (75kB)
     |████████████████████████████████| 81kB 94kB/s
Collecting pyasn1-modules (from service-identity->scrapy)
  Downloading https://files.pythonhosted.org/packages/be/70/e5ea8afd6d08a4b99ebfc77bd1845248d56cfcf43d11f9dc324b9580a35c/pyasn1_modules-0.2.6-py2.py3-none-any.whl (95kB)
     |████████████████████████████████| 102kB 146kB/s
Requirement already satisfied: setuptools in /usr/local/lib/python3.7/site-packages (from zope.interface>=4.4.2->Twisted>=13.1.0; python_version != "3.4"->scrapy) (41.0.1)
Collecting idna>=2.5 (from hyperlink>=17.1.1->Twisted>=13.1.0; python_version != "3.4"->scrapy)
  Downloading https://files.pythonhosted.org/packages/14/2c/cd551d81dbe15200be1cf41cd03869a46fe7226e7450af7a6545bfc474c9/idna-2.8-py2.py3-none-any.whl (58kB)
     |████████████████████████████████| 61kB 181kB/s
Requirement already satisfied: cffi!=1.11.3,>=1.8 in /usr/local/lib/python3.7/site-packages (from cryptography>=2.3->pyOpenSSL->scrapy) (1.12.3)
Requirement already satisfied: asn1crypto>=0.21.0 in /usr/local/lib/python3.7/site-packages (from cryptography>=2.3->pyOpenSSL->scrapy) (0.24.0)
Requirement already satisfied: pycparser in /usr/local/lib/python3.7/site-packages (from cffi!=1.11.3,>=1.8->cryptography>=2.3->pyOpenSSL->scrapy) (2.19)
Building wheels for collected packages: Twisted, PyDispatcher
  Building wheel for Twisted (setup.py) ... done
  Stored in directory: /Users/l/Library/Caches/pip/wheels/f4/2b/d5/bf550d6bead12fec7a1383be4e994758848c4aeeb9fc627ecf
  Building wheel for PyDispatcher (setup.py) ... done
  Stored in directory: /Users/l/Library/Caches/pip/wheels/88/99/96/cfef6665f9cb1522ee6757ae5955feedf2fe25f1737f91fa7f
Successfully built Twisted PyDispatcher
Installing collected packages: w3lib, lxml, zope.interface, constantly, incremental, attrs, Automat, idna, hyperlink, PyHamcrest, Twisted, cssselect, parsel, queuelib, pyasn1, pyasn1-modules, service-identity, PyDispatcher, scrapy
Successfully installed Automat-0.7.0 PyDispatcher-2.0.5 PyHamcrest-1.9.0 Twisted-19.7.0 attrs-19.1.0 constantly-15.1.0 cssselect-1.1.0 hyperlink-19.0.0 idna-2.8 incremental-17.5.0 lxml-4.4.1 parsel-1.5.2 pyasn1-0.4.6 pyasn1-modules-0.2.6 queuelib-1.5.0 scrapy-1.7.3 service-identity-18.1.0 w3lib-1.21.0 zope.interface-4.6.0
```

##  l@192  ~  cd /Users/l/Documents/Py/Pydemo
##  l@192  ~/Documents/Py/Pydemo  scrapy startproject firstscrapy


```
New Scrapy project 'firstscrapy', using template directory '/usr/local/lib/python3.7/site-packages/scrapy/templates/project', created in:
    /Users/l/Documents/Py/Pydemo/firstscrapy

You can start your first spider with:
    cd firstscrapy
    scrapy genspider example example.com
```

##  l@192  ~/Documents/Py/Pydemov cd firstscrapy
##  l@192  ~/Documents/Py/Pydemo/firstscrapy
