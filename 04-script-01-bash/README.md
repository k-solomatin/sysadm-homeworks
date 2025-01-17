# Домашнее задание к занятию "4.1. Командная оболочка Bash: Практические навыки"

## Обязательные задания

1. Есть скрипт:
	```bash
	a=1
	b=2
	c=a+b
	d=$a+$b
	e=$(($a+$b))
	```
	* Какие значения переменным c,d,e будут присвоены?
	* Почему?

1. На нашем локальном сервере упал сервис и мы написали скрипт, который постоянно проверяет его доступность, записывая дату проверок до тех пор, пока сервис не станет доступным. В скрипте допущена ошибка, из-за которой выполнение не может завершиться, при этом место на Жёстком Диске постоянно уменьшается. Что необходимо сделать, чтобы его исправить:
	```bash
	while ((1==1)
	do
	curl https://localhost:4757
	if (($? != 0))
	then
	date >> curl.log
	fi
	done
	```
1. Необходимо написать скрипт, который проверяет доступность трёх IP: 192.168.0.1, 173.194.222.113, 87.250.250.242 по 80 порту и записывает результат в файл log. Проверять доступность необходимо пять раз для каждого узла.

1. Необходимо дописать скрипт из предыдущего задания так, чтобы он выполнялся до тех пор, пока один из узлов не окажется недоступным. Если любой из узлов недоступен - IP этого узла пишется в файл error, скрипт прерывается

## Дополнительное задание (со звездочкой*) - необязательно к выполнению

Мы хотим, чтобы у нас были красивые сообщения для коммитов в репозиторий. Для этого нужно написать локальный хук для git, который будет проверять, что сообщение в коммите содержит код текущего задания в квадратных скобках и количество символов в сообщении не превышает 30. Пример сообщения: \[04-script-01-bash\] сломал хук.

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
# Домашка  
1.  
c = "a+b" - Это просто текст  
b = "1+3" - вывели просто значения, но не сложение   
e = "3"   - тут все норм, вывели значения и сложиили  
2.
```bash
while ((1==1))  
	 do  
			 curl https://localhost:4757  
			 if (($? != 0))  
			 then  
					 date >> curl.log  
			 else exit  
			 fi  
			 sleep 5  
```
3.  
```bash
hosts=(192.168.0.1 173.194.222.113 87.250.250.242)  
timeout=5  
for i in {1..5}  
do  
date >>hosts.log  
    for h in ${hosts[@]}  
    do  
			curl -Is --connect-timeout $timeout $h:80 >/dev/null  
        echo "    check" $h status=$? >>hosts.log  
    done  
done  
```
4.  
```bash
hosts=(192.168.0.1 173.194.222.113 87.250.250.242)  
timeout=5  
res=0  

while (($res == 0))  
do  
    for h in ${hosts[@]}  
    do  
	curl -Is --connect-timeout $timeout $h:80 >/dev/null  
	res=$?  
	if (($res != 0))  
	then  
	    echo "    ERROR on " $h status=$res >>hosts2.log  
	fi  
    done  
done  
```
end
