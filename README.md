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
виведення файлу хост для перегляду - у ньому запис блокатора - hosts очиститься після перезавантаження роутера - скрипт застосовувати повторно
* ** cat /etc/hosts
