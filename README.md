# drivers_PZ_2
## Подготовка файлов модуля
Создан файл `simple.c` с исходным кодом модуля ядра с помощью команды `nano simple.c`. Аналогично создан файл `Makefile` для сборки модуля
## Сборка модуля ядра
Выполнена команда для сборки модуля:
```
make
```
Вывод:
```
make -C /lib/modules/6.8.0-79-generic/build/ M=/home/drivers modules
make[1]: Entering directory '/usr/src/linux-headers-6.8.0-79-generic'
warning: the compiler differs from the one used to build the kernel
  The kernel was built by: x86_64-linux-gnu-gcc-13 (Ubuntu 13.3.0-6ubuntu2~24.04) 13.3.0
  You are using:           gcc-13 (Ubuntu 13.3.0-6ubuntu2~24.04) 13.3.0
  CC [M]  /home/drivers/simple.o
  MODPOST /home/drivers/Module.symvers
  CC [M]  /home/drivers/simple.mod.o
  LD [M]  /home/drivers/simple.ko
  BTF [M] /home/drivers/simple.ko
Skipping BTF generation for /home/drivers/simple.ko due to unavailability of vmlinux
make[1]: Leaving directory '/usr/src/linux-headers-6.8.0-79-generic'
```
## Загрузка модуля в ядро
Загрузка модуля с помощью команды:
``` 
sudo insmod simple.ko
```
Проверка загрузки модуля:
``` 
lsmod | grep simple
```
Вывод:
```
simple                 12288  0
```
Просмотр сообщений ядра с правами суперпользователя:
``` 
sudo dmesg | tail -5
```
Вывод:
```
[ 8333.460286] audit: type=1400 audit(1757929882.481:330): apparmor="DENIED" operation="mknod" class="file" profile="ubuntu_pro_esm_cache" name="/usr/lib/python3/dist-packages/uaclient/messages/__pycache__/__init__.cpython-312.pyc.131387074624816" pid=3367 comm="python3" requested_mask="c" denied_mask="c" fsuid=0 ouid=0
[ 8333.464749] audit: type=1400 audit(1757929882.485:331): apparmor="DENIED" operation="mknod" class="file" profile="ubuntu_pro_esm_cache" name="/usr/lib/python3/dist-packages/uaclient/messages/__pycache__/urls.cpython-312.pyc.131387074624816" pid=3367 comm="python3" requested_mask="c" denied_mask="c" fsuid=0 ouid=0
[10282.421904] simple: loading out-of-tree module taints kernel.
[10282.421910] simple: module verification failed: signature and/or required key missing - tainting kernel
[10282.422053] Hello from the mai 307 team
```
## Выгрузка модуля из ядра
``` 
sudo rmmod simple
```
Проверка сообщений ядра после выгрузки модуля:
``` 
sudo dmesg | tail -3
```
Вывод:
```
[10282.421910] simple: module verification failed: signature and/or required key missing - tainting kernel
[10282.422053] Hello from the mai 307 team
[10454.500293] Goodbye from the mai 307 team!
```
