# Лабораторная работа 2

## Скрипт

Сначала я посмотрел предложенные нам лекции. После, с помощью дополнительных источников, я написал следующий скрипт: 

```bash
#!/bin/bash

Validation() {
old_ifs=$IFS
IFS="."
error_message="\nНеверный формат ввода. IPv4-адрес имеет вид X.X.X.X, где X - целое число от 0 до 255 включительно\n"
pattern="([0-9]{1,3}[\.]){3}[0-9]{1,3}"
res=""
echo -n "Введите IPv4-адрес в десятичном формате: "
read address

if [[ $address =~ $pattern ]]; then
 for i in $address; do
 if [[ $i -ge 0 ]] && [[ $i -le 255 ]]; then
  t=$((echo "obase=2; $i" | bc))
   while [[ ${#t} -lt 8 ]]
   do
    t="0$t"
   done
  if [[ ${#res} -le 26 ]]; then
   res+="$t."
  else
   res+=$t
  fi
 else
  IFS=$old_ifs
  echo -e $error_message
  break
  Validation
  
 fi
 done
 if [[ ${#res} -eq 35 ]]; then
  IFS=$old_ifs
  echo $res
 else
  Validation
 fi
else
 IFS=$old_ifs
 echo -e $error_message
 Validation
fi
}


Validation
```

Пример входных данных:

```192.168.10.1```

Пример выходныx данных:

```11000000.10101000.00001010.00000001```

### Как успешно сдать работу?

Создать свой репозиторий из шаблона этого. Как это делается - "Use this template" -> "Create a new repository" и сделайте его public. 

Находясь уже в своем репозитории - создайте новый файл формата .md и там оформляйте отчет. В отчете опишите все шаги которые вы делали, чтобы получить финальный результат работы. Необходимы только скриншоты скрипта и примера его выполнения!

Что вам нужно знать, чтобы успешно защитить работу:

Переменные; как выполнять операции; условные конструкции; функции; циклы; как работать с массивом; как посмотреть права доступа к файлам; как выдавать права доступа; что такое и зачем нужен ip адрес и маска подсети.

## Дополнительные источники

1. [Присваивание значений переменным.](https://se.ifmo.ru/~ad/Documentation/ABS_Guide_ru.html#VARASSIGNMENT)
2. [Подстановка переменных.](https://se.ifmo.ru/~ad/Documentation/ABS_Guide_ru.html#VARSUBN)
3. [Арифметические операции.](https://se.ifmo.ru/~ad/Documentation/ABS_Guide_ru.html#ARITHEXP)
4. [Проверка условий.](https://se.ifmo.ru/~ad/Documentation/ABS_Guide_ru.html#TESTS)
5. stackoverflow.com
6. Хорошая ĸнига по Shell/bash в Linux - "Learn Linux Shell Scripting – Fundamentals of Bash 4.4" Sebastiaan
Tammer
7. [Функции.](https://se.ifmo.ru/~ad/Documentation/ABS_Guide_ru.html#FUNCTIONS)
8. [Функции и рекурсивные функции.](https://habr.com/ru/company/ruvds/blog/327248/)
9. [Циклы.](https://se.ifmo.ru/~ad/Documentation/ABS_Guide_ru.html#LOOPS)
10. [Массивы](https://se.ifmo.ru/~ad/Documentation/ABS_Guide_ru.html#ARRAYS)
11. [Про двоичную систему и IP-адрес](https://zametkinapolyah.ru/kompyuternye-seti/4-4-dvoichnye-chisla-i-dvoichnaya-sistema-schisleniya-perevod-chisla-v-dvoichnuyu-sistemu-schisleniya-iz-desyatichnoj.html)
12.  В. Олифер, Н. Олифер "Компьютерные сети. Принципы, технологии, протоколы. Учебник" (2016)
