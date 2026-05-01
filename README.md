# Lesson-8-system-boot

## Задание
- Включить отображение меню Grub.
- Попасть в систему без пароля несколькими способами.
- Установить систему с LVM, после чего переименовать VG.

```
#открываем конфиг
sadmin@lp-ubn1:~$ sudo nano /etc/default/grub
# меняем
#GRUB_TIMEOUT_STYLE=hidden
GRUB_TIMEOUT=10

#сохраняем, выходим, обновляем конфиг
sadmin@lp-ubn1:~$ sudo update-grub

#перезагружаемся, меню есть.
```

## вход в систему в обход пароля
```
# способ1 проверил, все ОК, попал в root@(none)
Способ 1: Через редактирование пункта меню GRUB (для Debian/Ubuntu)
В меню GRUB нажмите e для редактирования.
Найдите строку, начинающуюся с linux, и в параметрах ядра:
Замените ro на rw (чтение-запись).
Добавьте init=/bin/bash.
Нажмите Ctrl+X или F10 для загрузки.

#пароль сменил только мосле перемонтирования / c справами на чтение
mount -o remount,rw /

# перезагрузка сработала только в таком виде
reboot -f

#Способ2 проверил, он по ощущениям попроще

## Установить систему с LVM, после чего переименовать VG.
```
#проверяем сущеснтующую vg
sadmin@lp-ubn1:~$ sudo vgs
[sudo] password for sadmin:
  VG        #PV #LV #SN Attr   VSize   VFree
  ubuntu-vg   1   1   0 wz--n- <28.00g 14.00g

  # переименовываем VG
  sadmin@lp-ubn1:~$ sudo vgrename ubuntu-vg ubuntu-vg_v2
  Volume group "ubuntu-vg" successfully renamed to "ubuntu-vg_v2"

#меняем название в файле grub.cfg. 4-5 строк нашлось

#перезагружаемся, проверяем результат
sadmin@lp-ubn1:~$ sudo vgs
[sudo] password for sadmin:
  VG           #PV #LV #SN Attr   VSize   VFree
  ubuntu-vg_v2   1   1   0 wz--n- <28.00g 14.00g


```



```
