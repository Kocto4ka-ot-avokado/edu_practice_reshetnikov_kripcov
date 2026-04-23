## Bash скрипты.
### Используемое ПО:
1) ALT workstation 10.4;
2) VS code;
3) Библия

### Zero.sh

```
#!/bin/bash

group="321"
name="Костя"
surname="Решетников"
stipendia=748
usd_rate=90
usd_sum=$(echo "scale=2; $stipendia / $usd_rate" | bc)

echo "Я учусь в $group, зовут меня $name $surname. В этом месяце мне пришла стипендия размером в $stipendia рублей, это $usd_sum$."
```
<img width="816" height="102" alt="image" src="https://github.com/user-attachments/assets/39707dc1-8ab4-4ed7-8aff-e285a037ba15" />

*Рис.1 Выполнение zero.sh*

### Start.sh

```
#!/bin/bash

echo "Привет, $1!"
```
<img width="344" height="34" alt="image" src="https://github.com/user-attachments/assets/33de3676-a13b-4a1d-aa92-84a0b9bf690c" />

*Рис.2 Выполнение start.sh*

## start_2.sh

```
#!/bin/bash

if [ -n "$1" ]; then
    echo "Привет, $1!"
else
    echo "Имя не передано."
fi
```

<img width="358" height="38" alt="image" src="https://github.com/user-attachments/assets/464f23c3-acba-41bd-8279-0a7cea821c71" />

*Рис.3 Выполнение start_2.sh*

### file.sh

```
#!/bin/bash

if [ -e "$1" ]; then
    echo "Файл '$1' существует."
else
    echo "Файл '$1' не найден."
fi
```

<img width="560" height="87" alt="image" src="https://github.com/user-attachments/assets/2cbb39b4-8e1a-41fa-b42a-b1f23be3e151" />

*Рис.4 Выполнение file.sh*

### my_dir.sh

#!/bin/bash

if [ -d "$1" ]; then
    ls "$1"
else
    echo "Директория '$1' не найдена."
fi

<img width="611" height="48" alt="image" src="https://github.com/user-attachments/assets/d8acc642-8ff3-4a87-888a-90e687ec6efe" />
*Рис.5 Выполнение my_dir.sh*

### dir_m.sh

#!/bin/bash

if [ -d "$1" ]; then
    echo "Директория '$1' уже существует."
else
    mkdir "$1"
    echo "Директория '$1' создана."
fi

<img width="860" height="49" alt="image" src="https://github.com/user-attachments/assets/54ab6973-cb19-41da-bc1c-481079926aa9" />

*Рис.6 выполнение dir_m.sh*


### user_light.sh

#!/bin/bash

my_user=$(whoami)
if grep -q "^$my_user:" /etc/passwd; then
    echo "Поздравляю! Пользователь '$my_user' найден в системе."
fi

<img width="507" height="42" alt="image" src="https://github.com/user-attachments/assets/2ba0e902-02d8-4394-a413-b6dc6e92acbf" />

*Рис.7 вполнение user_light.sh*

### user_f.sh

#!/bin/bash

if grep -q "^$1:" /etc/passwd; then
    echo "Пользователь '$1' найден."
else
    echo "Пользователь '$1' не найден."
fi

<img width="515" height="51" alt="image" src="https://github.com/user-attachments/assets/f2b6dc24-3417-4b6e-b5b8-6dbf44c54f45" />

*Рис.8 Выполение user_f.sh*

### uer_f2.sh



*Рис.9 Выполение user_f2.sh*

### finder_liight.sh

#!/bin/bash

if [ -f "$1" ]; then
    echo "'$1' — обычный файл."
elif [ -d "$1" ]; then
    echo "'$1' — директория."
elif [ -L "$1" ]; then
    echo "'$1' — символическая ссылка."
else
    echo "'$1' — не существует или другой тип."
fi

<img width="603" height="77" alt="image" src="https://github.com/user-attachments/assets/8590d82c-d3e6-4aa9-b6bf-40bbd5b36649" />

*Рис.10 Выполнение finder_liight.sh*

### math.sh

#!/bin/bash

a=$1
b=$2

echo "Сумма: $((a + b))"
echo "Разность: $((a - b))"
echo "Произведение: $((a * b))"

<img width="462" height="205" alt="image" src="https://github.com/user-attachments/assets/312b0590-8f66-484f-9fb6-cd4e67cd32d2" />

*Рис.11 Выполнение math.sh*

### sort.sh

```
#!/bin/bash

for arg in "$@"; do
    echo "$arg"
done****
```

<img width="522" height="132" alt="image" src="https://github.com/user-attachments/assets/c3ee63e0-0edb-4325-9aa5-6c84494331f5" />

*Рис.12 Выполнение sort.sh*

### io.sh

```
#!/bin/bash

case "$1" in
    start) echo "Starting..." ;;
    stop)  echo "Stopping..." ;;
    *)     echo "Используй: $0 {start|stop}" ;;
esac
```

<img width="504" height="223" alt="image" src="https://github.com/user-attachments/assets/3b72af14-48c8-47e8-835d-b92070e54867" />

*Рис.13 Выполнение io.sh*

### user_use.sh

```
#!/bin/bash

du -sk /home/* 2>/dev/null | sort -nr | while read size dir; do
    user=$(basename "$dir")
    echo "$user — $size КБ"
done
```

<img width="580" height="69" alt="image" src="https://github.com/user-attachments/assets/130a8fef-ecbf-4cf4-b178-0cc87083c460" />

*Рис.14 Выполнение user_use*

### sort_du.sh

```
#!/bin/bash

dir="${1:-.}"
find "$dir" -type f -printf '%T@ %p\n' 2>/dev/null | sort -n | head -3 | while read timestamp path; do
    date=$(date -d "@$timestamp" "+%Y-%m-%d %H:%M:%S")
    echo "$path — $date"
done
```

*Рис 15. Выполнение sort_du*

### dir_info.sh

```
#!/bin/bash

dir="${1:-.}"
size=$(du -sk "$dir" | awk '{print $1}')
echo "Общий размер: $size КВ"
```

<img width="720" height="104" alt="image" src="https://github.com/user-attachments/assets/7d1d0d8a-7f43-4cb8-9741-0579955b34d1" />

*Рис.16 Выполнение dir_info.sh*

### bash+history.sh

```
#!/bin/bash

hist_file="$HOME/.bash_history"
if [ -f "$hist_file" ]; then
    awk '{print $1}' "$hist_file" | sort | uniq -c | sort -nr | head -5
else
    echo "Файл .bash_history не найден."
fi
```

<img width="675" height="199" alt="image" src="https://github.com/user-attachments/assets/d86810f3-4d8c-4150-8e6d-7839eab4b755" />


*Рис.17 Вполнение bash_history.sh*
