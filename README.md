# -kill-analytics-Xiaomi-BE3600
Скрипт Xiaomi BE3600, засліплює шпигунів Xiaomi, вбиває їх активні процеси та звільняє оперативну пам'ять для більш швидкої роботи.
[color="#000000"][b][color=blue][center][size=4]SSH
Скрипт ослепляет шпионов Xiaomi, убивает их активные процессы и освобождает оперативную память для более быстрой работы.[/size][/center][/color][/b]
[color="#000000"]Блокировка серверов (echo...>>/etc/hosts): Прописывает в систему, что адреса сбора статистики Xiaomi находятся «внутри» роутера (127.0.0.1). Теперь данные не могут вылететь в интернет – они стучат в закрытую дверь.
Расстрел процессов (killall -9…): мгновенно убивает службы, отвечающие за сбор логов и отчетов (milog, stat_chain). Это высвобождает ресурсы процессора.
Сохранение (sync): Принудительно записывает все изменения на диск/память, чтобы ничего не "зависло" в очереди.
Очистка кэша (echo 3 > ...drop_caches): Выгружает из оперативной памяти ненужный мусор, который там накопился.
Отчет (free -m и echo Temp): отображение реального остатка свободной памяти и точной температуры процессора.[/color][/color]
[color=silver]в шапку[/color]
[spoiler][attachment="34992754:2026-2-22_17-37-27.png"][/spoiler]
[spoiler=скрипт full][code]echo "127.0.0.1 data.mistat.xiaomi.com log.ad.xiaomi.com stat.miwifi.com api.miwifi.com" >> /etc/hosts && killall -9 miwifi-logd milog stat_chain 2>/dev/null; sync && echo 3 > /proc/sys/vm/drop_caches && free -m && echo "Temp: $(( $(cat /sys/class/thermal/thermal_zone0/temp) / 1000 ))°C"
[spoiler=монитор свободной ram памяти][code]free -m[/code][/spoiler]
[spoiler=монитор температуры процессора][code]echo $(($(cat /sys/class/thermal/thermal_zone0/temp) / 1000))°C[/code][/spoiler]
[spoiler=монитор частота процессора]cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq[/spoiler]
[spoiler=вывод файла хост для просмотра - в нем запись блокиратора - hosts очистится после перезагрузки роутера - скрипт применять повторно][code]cat /etc/hosts[/code][/spoiler]
