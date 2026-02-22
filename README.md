# -kill-analytics-Xiaomi-BE3600
Скрипт Xiaomi BE3600, засліплює шпигунів Xiaomi, вбиває їх активні процеси та звільняє оперативну пам'ять для більш швидкої роботи.

Скрипт засліплює шпигунів Xiaomi, вбиває їх активні процеси і звільняє оперативну пам'ять для швидшої роботи. 
Тепер дані не можуть вилетіти в інтернет – вони стукають у зачинені двері.
Розстріл процесів (killall -9…): миттєво вбиває служби, які відповідають за збирання логів та звітів (milog, stat_chain). 
Це звільняє ресурси процесора.
Збереження (sync): Примусово записує всі зміни на диск/пам'ять, щоб нічого не зависло в черзі.
Очищення кешу (echo 3 > ...drop_caches): Вивантажує з оперативної пам'яті непотрібне сміття, яке там накопичилося.
Отчет (free -m и echo Temp): отображение реального остатка свободной памяти и точной температуры процессора.

---
скрипт full 
* ** echo "127.0.0.1 data.mistat.xiaomi.com log.ad.xiaomi.com stat.miwifi.com api.miwifi.com" >> /etc/hosts && killall -9 miwifi-logd milog stat_chain 2>/dev/null; sync && echo 3 > /proc/sys/vm/drop_caches && free -m && echo "Temp: $(( $(cat /sys/class/thermal/thermal_zone0/temp) / 1000 ))°C" && echo "Freq: $(( $(cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq) / 1000 )) MHz"
---
очищення кешу пам'яті
* ** echo 3 > /proc/sys/vm/drop_caches
---
монітор вільної RAM пам'яті
* ** free -m
---
монітор температури процесора
* ** cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq
---
монітор частота процесора
* ** cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq
---
виведення файлу хост для перегляду - у ньому записи блокіровки - hosts очиститься після перезавантаження роутера - застосовувати повторно
* ** cat /etc/hosts
---
Перевірка data info
* ** bdata show
---

Перевірка блокування телеметрії:
* ** ping data.mistat.xiaomi.com
Має показувати PING data.mistat.xiaomi.com (127.0.0.1).
---

очищення кешу пам'яті: 
* ** echo 3 > /proc/sys/vm/drop_caches
---

Перевірка вільної пам'яті:
* ** free -m
63836 - 68504 зафіксовано
---

частота процесора
* ** cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq
---

Температура процесора (якщо підтримується моделлю):
* ** t_sensor
або
* ** cat /sys/class/thermal/thermal_zone0/temp
* ** echo $(cat /sys/class/thermal/thermal_zone0/temp | cut -c1-2)°C
* ** echo $(($(cat /sys/class/thermal/thermal_zone0/temp) / 1000))°C
 62000 зафіксовано 65700
---

Перевірка вмісту hosts (чи нічого не злетіло):
* ** cat /etc/hosts
---

Перевірка останніх подій у системі:
* ** dmesg | tail -n 20
---

Навантаження на процесор в реальному часі:
* ** top
(Натисни Q, щоб вийти. Дивись на CPU usage та процеси, які їдять найбільше).
---

Статус Wi-Fi клієнтів (хто підключений і з яким сигналом):
* ** iwinfo
---

Перевірка аптайму (скільки працює без перезавантаження):
* ** uptime
---
