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
