## Лабораторная работа No2

**Задание 1:**

1\. Создание файла *a.bash23* :

Откройте терминал и выполните команду для создания нового файла *a.bash23*:

```bash
touch a.bash23
```

Результат :

`root@LAPTOP-AJ4C61LN:~# touch a.bash23`

2\. Открытие и редактирование файла :

В терминале выполните команду для открытия файла в текстовом редакторе:  `gedit a.bash23`

```bash
gedit a.bash23
```

Результат :

`root@LAPTOP-AJ4C61LN:~# gedit a.bash23`

3\. Напишите код для файла :

В файле *a.bash23*, введите следующий код :

```bash
if [[ $a -eq 23 ]]
   then
     echo "Modify me!"
   else
     echo '$a is not "23"'
   fi
```

Результат :

![image](https://github.com/haha523/lab_2.linux/blob/29b03824217f440bb9629207708c1cbb9779413d/png%20for%20linux2/png%20code%202.1.png).

4\. Запустите сценарий :

Вернитесь в Terminal и введите следующую команду, чтобы запустить сценарий :      `root@LAPTOP-AJ4C61LN:~# bash a.bash23`

```bash
bash a.bash23
```

![image](https://github.com/haha523/lab_2.linux/blob/29b03824217f440bb9629207708c1cbb9779413d/png%20for%20linux2/png%20for%20input%202.1.png).

Результат :


```bash
$a is not "23"
```


`root@LAPTOP-AJ4C61LN:~# touch a.bash23`

`root@LAPTOP-AJ4C61LN:~# gedit a.bash23`

`root@LAPTOP-AJ4C61LN:~# bash a.bash23`

`$a is not "23"`

**Задание 2:**

1\. Создание файла *ip.bash* :

Откройте терминал и выполните команду для создания нового файла *ip.bash*:

```bash
touch ip.bash
```

Результат :

`root@LAPTOP-AJ4C61LN:~# touch ip.bash`

2\. Открытие и редактирование файла :

В терминале выполните команду для открытия файла в текстовом редакторе:  `gedit ip.bash`

```bash
gedit ip.bash
```

3\. Напишите код для файла :

В файле *ip.bash*, введите следующий код :

```bash
#!/bin/bash

if [ "$#" -ne 1 ]; then
    echo "Используйте: $0 <IPv4-адрес>"
    exit 1
fi

ip_address=$1

IFS='.' read -r -a octets <<< "$ip_address"

if [ "${#octets[@]}" -ne 4 ]; then
    echo "Некорректный формат IPv4-адреса."
    exit 1
fi

binary_octets=()

for octet in "${octets[@]}"; do
    if ! [[ "$octet" =~ ^[0-9]+$ ]] || [ "$octet" -lt 0 ] || [ "$octet" -gt 255 ]; then
        echo "Недопустимое значение октета: $octet. Октет должен быть числом от 0 до 255."
        exit 1
    fi

    binary_octet=$(printf "%08d" "$(bc <<< "obase=2;$octet")")
    binary_octets+=("$binary_octet")
done

binary_ip=$(IFS=.; echo "${binary_octets[*]}")

echo "$binary_ip"
```

Результат :

![image](https://github.com/haha523/lab_2.linux/blob/b1ae0d4a5e858c6e07add506feb485673c4b355b/png%20for%20linux2/png%20code%20linux%202.2.png).


4\. Сделайте файл исполняемым :

Введите следующую команду, чтобы запустить сценарий :      `root@LAPTOP-AJ4C61LN:~# chmod +x ip.bash`

```bash
chmod +x ip.bash
```

5\. Запустите скрипт с IPv4-адресом в качестве аргумента :

Введите следующую команду, чтобы запустить сценарий :   ` root@LAPTOP-AJ4C61LN:~# ./ip.bash 192.168.10.1`

```bash
./ip.bash 192.168.10.1

```

Результат :

```bash
11000000.10101000.00001010.00000001

```


![image](https://github.com/haha523/lab_2.linux/blob/f6b580b4c194262d2850dfa33a05517cce78897c/png%20for%20linux2/png%20for%20input%202.2.png).

`root@LAPTOP-AJ4C61LN:~# touch ip.bash`

`root@LAPTOP-AJ4C61LN:~# gedit ip.bash`

`root@LAPTOP-AJ4C61LN:~# chmod +x ip.bash`

`root@LAPTOP-AJ4C61LN:~# ./ip.bash 192.168.10.1`

`11000000.10101000.00001010.00000001`



