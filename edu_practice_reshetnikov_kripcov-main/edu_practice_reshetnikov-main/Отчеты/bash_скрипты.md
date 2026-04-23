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


*Рис.1 Выполнение zero.sh*

### Start.sh

```
#!/bin/bash

echo "Привет, $1!"
```

*Рис.2 Выполнение start.sh*

## Привет
