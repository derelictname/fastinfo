# about

Раньше с компьютерами общались через перфокарты, потом перешли на терминалы - отдельные от компьютера самостоятельные устройства из клавиатуры и монитора для передачи текста в компьютер и обратно. Первыми терминалами были телетайпы, так как они уже были изобретены в телеграфии. Но со временем их превратили в видеотерминалы, заменили печатные ленты на ЭЛТ, добавили микропроцессор.

Терминал подключался через UART порт. Драйвер порта в операционной системе имел буфер для операций над передаваемым текстом (редактирование, отображение ввода, перенос строки), который мог отключаться, например, для текстовых редакторов, и драйвер TTY для управления сеансом обмена текстом (определет какая программа получит ввод и от какой программы принять ответ). В Unix драйвер порта управлялся через устройство TTY в папке /dev/. Программа login передаёт права на файл пользователю, вошедшему в систему через конкретный терминал.

Сейчас вместо физического терминала и UART порта используется эмулятор терминала. Для общения с программой он создаёт виртуальный терминал - псевдотерминал. Через функцию `int posix_openpt(int flags)` создаётся файл в /dev/pts/ (slave) и возвращается файловый дескриптор master. Эмулятор терминала соединяется с master, master - со slave через Unix socket, а slave - с программой. Таким образом между эмулятором терминала и программой двухсторонний текстовый обмен.

Также из прошлого остались виртуальные терминалы,  доступные по нажатию кобинаций Alt+F1 - F7.

Узнать терминал текущего процесса

    tty

Вывод настроек терминала

    stty -a

Отключить автоперевод длинных строк

    tput rmam
    man 5 terminfo
    man termcap
    man tput

Кол-во псевдотерминалов

    echo "$(cat /proc/sys/kernel/pty/nr)/$(cat /proc/sys/kernel/pty/max)"

Эмулятор терминала в ретро стиле

    apt install cool-retro-term

Вставка управляющих символов

    Ctrl + v
    Ctrl + g

Стереть слово

    Ctrl + w

## X-terminal

Помимо текстовых терминалов были ещё и Х-терминалы, соединявшиеся с X Window System по протоколу X11, но из-за появления в компьютерах видеокарт и периферийных устройств Х-терминалы стали не нужны, код X Window System перестал поддерживаться, все просто надстраивают костыли над ним. Поэтому появился Wayland, в котором убраны лишние слои абстракции от железа, окна напрямую отрисовываются в видеодрайвере, что повышает отзывчивость интерфейса.

