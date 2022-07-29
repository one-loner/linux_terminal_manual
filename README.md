# linux_terminal_manual
Оболочки linux:  
The Bourne shell        /bin/sh  
The Bourne again shell  /bin/bash  
The Korn shell          /bin/ksh  
The C Shell             /bin/csh  
Tom's C Shell           /bin/tcsh  
***
Команды:  
cat - вывод содержимого файла в консоль  
cd - переход в каталог  
ls - вывод содержимого каталога  
echo - вывод текста в консоль  
touch - обновление времени редактирования файла либо создание файла если файла нет  
file - справка по файлу  
whatis - справка по названию  
history - вывод истрии команд  
env - вывод переменных среды  
pwd - текущий каталог  
export - задание переменной  
unset - отключение переменной  
mkdir - создать папку  
rmdir - удалить папку  
cp - копирование файлов и папок  
mv - перемещение файлов и папок (так же её используют для переименования)  
При копировании папок командами cp и mv используется ключ -R (Рекурсивное копирование/перемещение)  
rm - удаление файлов и папок (для удаления папок с содержимым использовать ключ -rf)   
Посмотреть используемую оболочку:  
cat /etc/passwd  

Глобальные настройка bash находятся в файле /etc/profile.  
Настройки bash для конкретного пользователя /home/<username>/.profile  
Настройка внешнего вида консоли для конкретного пользователя /home/<username>/.bashrc  

Несколько команд в одной строке comand1 ; comand2  
Например: ls ; pwd  
Вывод по маске:  
ls *.txt  

Информация о системе:  
uname -a  

Найти мануалы, связанные с http man -k http  

Выполнить команду, игнорируя настройки оболочки exec  

Групповые символы:  
* - любая последовательность символов, включая пустую последовательность.  
? - один любой символ  
! - не  
[ac] - а или c  
[a-c] - a,b,c  

Команда для поиска find  
find /path/ - name "Something*"  
find /path/ -size +7M  
find /path/ -size -7M  
find /path/ -type d    - Найти директорию  
find /path/ -type f    - Найти файл  
find /path/ -atime +5  - Найти по времени доступа [дней]  
find /path/ -ctime +5  - Найти по времени создания [дней]  

Архиваторы:  
cpio - копирует файлы из и в архивы  
ls | cpio -o > /path/archive.cpio  - Архивирует содержимое папки в архив по соответствующему адресу.  
find . -name "*.txt" | cpio -o > /path/archive1.cpio -  Архивирует файлы в папке с расширением .txt в архив по соответствующему адресу.  
cpio -id < /path/to/archive.cpio - извлечь архив из в текущую папку  


dd - конвертирует и копирует файлы. Может копировать блочные устройства (Диски и т.д.) Для работы программы нужны права root  

dd if=/dev/sdb of=drive.img  Взять диск sdb и записать в файл drive.img  

gzip - архиватор  
gizp file - создаёт архив c расширением .gz , удаляя оригинал файла  
gunzip file.gz - распаковывает архив file.gz , удаляя оригинал архива.  

bzip2 - архиватор  
bizp2 file - создаёт архив c расширением .bz2 , удаляя оригинал файла  
bunzip2 file.bz2 - распаковывает архив file.bz2 , удаляя оригинал архива.  

bzip2 сжимает файлы гораздо эффективнее, чем gzip  

xz - архиватор, создающий контейнер для одного единственного файла.  
xz file - создаёт архив c расширением .xz , удаляя оригинал файла  
xz file.xz - распаковывает архив file.xz , удаляя оригинал архива.  


tar - наиболее часто используемый архиватор.   
tar cvf archive.tar folder    - Заархивировать папку folder в архив archive.tar. Оригинал папки folder сохраняется.   
tar cvfz archive.tar.gz folder    - Заархивировать папку folder в архив archive.tar.gz, используя архиватор gzip Оригинал папки folder сохраняется.  
tar xvf archive.tar - Разархивировать archive.tar в текущую папку.  

Потоки, конвееры и перенаправления ввода/вывода.  

> Передать в (Если указан имеющийся файл, то его содержимое будет перезаписано.  
>> Дописать в  
< Взять из  
| Передать сдедующей команде  
Tee отправить файл на стандартный вывод.  
xargs - построчно передать на вывод команде.  

Вывод ошибки в файл comand 2> error.txt  
Comand > result.txt 2>error.txt  -  Вывод резултата в файл result.txt, а ошибку в error.txt  

Comand1 |Comand2 - Передать результат команды 1 как входные данные для команды 2  

ls | grep r - Найти в текущей папке файлы с буквой r  

ls | tee output.txt - Вывести содержимое папки на экран  

find . -name "*.txt" | xargs cat - Вывести на экран содержимое всех текстовых файлов на экран   

Управление службами:   
systemctl list-units --all --type=service  
                                         - Показать список запущеных служб  
service  --status-all    


systemctl start application - Запуск службы  
systemctl stop application  - Остановка службы  
systemctl restart application - Перезапуск службы  
systemctl reload application - Перезагрузка службы  
systemctl status application - Показать статус службы  
systemctl list-unit-files --state enabled - Показать список служб в автозагрузке.  
systemctl enable application  - Добавить службу в автозагрузку  
systemctl disable application - Убрать службу из автозагрузки  
systemctl is-enabled application - Показать, есть ли служба в автозагрузке.  

