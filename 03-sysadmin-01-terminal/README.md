# Домашнее задание к занятию "3.1. Работа в терминале, лекция 1"

1. Установите средство виртуализации [Oracle VirtualBox](https://www.virtualbox.org/).

1. Установите средство автоматизации [Hashicorp Vagrant](https://www.vagrantup.com/).

1. В вашем основном окружении подготовьте удобный для дальнейшей работы терминал. Можно предложить:

	* iTerm2 в Mac OS X
	* Windows Terminal в Windows
	* выбрать цветовую схему, размер окна, шрифтов и т.д.
	* почитать о кастомизации PS1/применить при желании.

	Несколько популярных проблем:
	* Добавьте Vagrant в правила исключения перехватывающих трафик для анализа антивирусов, таких как Kaspersky, если у вас возникают связанные с SSL/TLS ошибки,
	* MobaXterm может конфликтовать с Vagrant в Windows,
	* Vagrant плохо работает с директориями с кириллицей (может быть вашей домашней директорией), тогда можно либо изменить [VAGRANT_HOME](https://www.vagrantup.com/docs/other/environmental-variables#vagrant_home), либо создать в системе профиль пользователя с английским именем,
	* VirtualBox конфликтует с Windows Hyper-V и его необходимо [отключить](https://www.vagrantup.com/docs/installation#windows-virtualbox-and-hyper-v),
	* [WSL2](https://docs.microsoft.com/ru-ru/windows/wsl/wsl2-faq#does-wsl-2-use-hyper-v-will-it-be-available-on-windows-10-home) использует Hyper-V, поэтому с ним VirtualBox также несовместим,
	* аппаратная виртуализация (Intel VT-x, AMD-V) должна быть активна в BIOS,
	* в Linux при установке [VirtualBox](https://www.virtualbox.org/wiki/Linux_Downloads) может дополнительно потребоваться пакет `linux-headers-generic` (debian-based) / `kernel-devel` (rhel-based).

1. С помощью базового файла конфигурации запустите Ubuntu 20.04 в VirtualBox посредством Vagrant:

	* Создайте директорию, в которой будут храниться конфигурационные файлы Vagrant. В ней выполните `vagrant init`. Замените содержимое Vagrantfile по умолчанию следующим:

		```bash
		Vagrant.configure("2") do |config|
			config.vm.box = "bento/ubuntu-20.04"
		end
		```

	* Выполнение в этой директории `vagrant up` установит провайдер VirtualBox для Vagrant, скачает необходимый образ и запустит виртуальную машину.

	* `vagrant suspend` выключит виртуальную машину с сохранением ее состояния (т.е., при следующем `vagrant up` будут запущены все процессы внутри, которые работали на момент вызова suspend), `vagrant halt` выключит виртуальную машину штатным образом.

1. Ознакомьтесь с графическим интерфейсом VirtualBox, посмотрите как выглядит виртуальная машина, которую создал для вас Vagrant, какие аппаратные ресурсы ей выделены. Какие ресурсы выделены по-умолчанию?

1. Ознакомьтесь с возможностями конфигурации VirtualBox через Vagrantfile: [документация](https://www.vagrantup.com/docs/providers/virtualbox/configuration.html). Как добавить оперативной памяти или ресурсов процессора виртуальной машине?

1. Команда `vagrant ssh` из директории, в которой содержится Vagrantfile, позволит вам оказаться внутри виртуальной машины без каких-либо дополнительных настроек. Попрактикуйтесь в выполнении обсуждаемых команд в терминале Ubuntu.

1. Ознакомиться с разделами `man bash`, почитать о настройках самого bash:
    * какой переменной можно задать длину журнала `history`, и на какой строчке manual это описывается?
    * что делает директива `ignoreboth` в bash?
1. В каких сценариях использования применимы скобки `{}` и на какой строчке `man bash` это описано?
1. Основываясь на предыдущем вопросе, как создать однократным вызовом `touch` 100000 файлов? А получилось ли создать 300000?
1. В man bash поищите по `/\[\[`. Что делает конструкция `[[ -d /tmp ]]`
1. Основываясь на знаниях о просмотре текущих (например, PATH) и установке новых переменных; командах, которые мы рассматривали, добейтесь в выводе type -a bash в виртуальной машине наличия первым пунктом в списке:

	```bash
	bash is /tmp/new_path_directory/bash
	bash is /usr/local/bin/bash
	bash is /bin/bash
	```

	(прочие строки могут отличаться содержимым и порядком)

1. Чем отличается планирование команд с помощью `batch` и `at`?

1. Завершите работу виртуальной машины чтобы не расходовать ресурсы компьютера и/или батарею ноутбука.


 ---

### Как оформить ДЗ!!!?

Домашнее задание выполните в файле readme.md в github репозитории. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.

Также вы можете выполнить задание в [Google Docs](https://docs.google.com/document/u/0/?tgif=d) и отправить в личном кабинете на проверку ссылку на ваш документ.
Название файла Google Docs должно содержать номер лекции и фамилию студента. Пример названия: "1.1. Введение в DevOps — Сусанна Алиева"
Перед тем как выслать ссылку, убедитесь, что ее содержимое не является приватным (открыто на комментирование всем, у кого есть ссылка).
Если необходимо прикрепить дополнительные ссылки, просто добавьте их в свой Google Docs.

Любые вопросы по решению задач задавайте в чате Slack!!!.

---
Решение ДЗ.
------
1. VirtualBox установил.
```bash
brew install virtualbox
```
2. Vagrant установил
```bash
brew install vagrant
brew install vagrant-manager
```
3. Работаю на маке - поэтому iTerm2
4. Виртуальную машину создал, базовые клманды выполнил
```bash
~/vagrant ❯ vagrant up                                                                   
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Checking if box 'bento/ubuntu-20.04' version '202107.28.0' is up to date...
==> default: Resuming suspended VM...
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
==> default: Machine booted and ready!
==> default: Machine already provisioned. Run `vagrant provision` or use the `--provision`
==> default: flag to force provisioning. Provisioners marked to run always will still run.
~/vagrant ❯ vagrant suspend                                                
==> default: Saving VM state and suspending execution...
~/vagrant ❯ vagrant halt      
==> default: Attempting graceful shutdown of VM...
```
5. Ознакомился.
По умолчанию для виртуалки хар-ки такие :
```
Оперативная память - 1гб
Видео - 4мб
Диск - 64гб
```
6. Для добавления памяти и проца нужно дописать в Vagrantfile :
```
config.vm.provider "virtualbox" do |v|
  v.memory = 2048
  v.cpus = 4
end
```
7. Практика команд на виртуалке
```
~/vagrant ❯ vagrant ssh                                     
Welcome to Ubuntu 20.04.2 LTS (GNU/Linux 5.4.0-80-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Thu 05 Aug 2021 03:23:24 PM UTC

  System load:  0.0               Processes:             114
  Usage of /:   2.5% of 61.31GB   Users logged in:       0
  Memory usage: 14%               IPv4 address for eth0: 10.0.2.15
  Swap usage:   0%


This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento
Last login: Thu Aug  5 09:31:37 2021 from 10.0.2.2
vagrant@vagrant:~$ date
Thu 05 Aug 2021 03:23:30 PM UTC
vagrant@vagrant:~$ ls -lah
total 2.7M
drwxr-xr-x 4 vagrant vagrant 2.7M Aug  5 06:14 .
drwxr-xr-x 3 root    root    4.0K Jul 28 17:50 ..
-rw------- 1 vagrant vagrant  439 Aug  5 06:28 .bash_history
-rw-r--r-- 1 vagrant vagrant  220 Jul 28 17:50 .bash_logout
-rw-r--r-- 1 vagrant vagrant 3.7K Jul 28 17:50 .bashrc
drwx------ 2 vagrant vagrant 4.0K Jul 28 17:51 .cache
-rw-r--r-- 1 vagrant vagrant  807 Jul 28 17:50 .profile
drwx------ 2 vagrant root    4.0K Aug  5 05:44 .ssh
-rw-r--r-- 1 vagrant vagrant    0 Jul 28 17:51 .sudo_as_admin_successful
-rw-r--r-- 1 vagrant vagrant    6 Jul 28 17:51 .vbox_version
-rw-r--r-- 1 root    root     180 Jul 28 17:55 .wget-hsts
vagrant@vagrant:~$ uptime
 15:23:50 up 0 min,  1 user,  load average: 0.00, 0.00, 0.00
vagrant@vagrant:~$ sudo ntpdate pool.ntp.org
 5 Aug 15:24:49 ntpdate[1119]: step time server 194.190.168.1 offset 2.156622 sec
vagrant@vagrant:~$
```
8. C разделами bash ознакомился.
Какой переменной можно задать длину журнала history, и на какой строчке manual это описывается? -
```
HISTFILESIZE
              The maximum number of lines contained in the history file.  When this variable is assigned a value, the history file is truncated, if necessary, by removing the oldest
              entries, to contain no more than that number of lines.  The default value is 500.  The history file is also truncated to this size after writing it when an interactive
              shell exits.

```

Что делает директива ignoreboth в bash? -
```
ignoreboth — не записывать команду, которая начинается с пробела, либо команду, которая дублирует предыдущую.
# export HISTCONTROL=ignoreboth.
```
9. сценарий списка или перечисления, сокращения.

```
function name [()] compound-command [redirection]
              This  defines  a  function named name.  The reserved word function is optional.  If the function reserved word is supplied, the parentheses are optional.  The body of the function is
              the compound command compound-command (see Compound Commands above).  `That command is usually a list of commands between { and }`, but may be any command listed  under  Compound  Com‐
              mands  above, with one exception: If the function reserved word is used, but the parentheses are not supplied, the braces are required.  compound-command is executed whenever name is
              specified as the name of a simple command.  When in posix mode, name may not be the name of one of the POSIX special builtins.  Any redirections  (see  REDIRECTION  below)  specified
              when a function is defined are performed when the function is executed.  The exit status of a function definition is zero unless a syntax error occurs or a readonly function with the
              same name already exists.  When executed, the exit status of a function is the exit status of the last command executed in the body.  (See FUNCTIONS below.)
```

10. Создать 100000 файлов
```
vagrant@vagrant:~$ touch file{1..100000}
vagrant@vagrant:~$ ls | wc -l
100000
vagrant@vagrant:~$
```
Создать 300000 файлов
```
vagrant@vagrant:~$ touch file{1..300000}
-bash: /usr/bin/touch: Argument list too long
```
11. Истина если файл присутствует или является каталогом.

12. Добавление переменной
```
mkdir /tmp/new_path_directory/
cp /usr/bin/bash /tmp/new_path_directory/
export PATH=/tmp/new_path_directory/:$PATH

```


13. at используется для назначения одноразового задания на заданное время, а batch — для назначения одноразовых задач, которые должны выполняться, когда загрузка системы становится меньше 0,8.

14. vagrant halt
