# ZX_Keyboard_PS-2_on_CPLD
Адаптер PS/2 клавиатуры для ZX Spectrum совместимых компьютеров на CPLD.

Данный адаптер я разработал специально для Ленинград 1, поэтому он может быть установлен на штатный разъём подключения клавиатуры и разъём Kempston джойстика. Для этого необходима минимальная доработка: на свободные контактв разъёма клавиатуры (7,8) необходимо подключить питание 5 вольт плюс и минус соответственно. Вживую адаптер выглядит следующим образом:
![Image](https://github.com/AndrejChoo/ZX_Keyboard_PS-2_on_CPLD/blob/main/hardware/image/PS_2_On_Leningrad1.jpg)

В основе адаптера находится CPLD Altera MAX2 EPM240 на 240 макроячеек. В ней реализован как сам PS/2 контроллер, так и матрица спектрумовской клавиатуры с транслятором сканкодов PS/2 в имитацию нажатия клавиш клавиатуры и кнопок Kempston джойстика. Также реализованы функции RESET и NMI (назначены на кнопки F1, F12), правда для работы этих функций будет необходимо подпаиваться проводами к плате, так как на разъём клавиатуры соответствующие сигналы не выведены. 
Также на плате адаптера есть кварцевый генератор (в данном случае на 50MHz), благодаря этому адаптер будет одинаково работать как на обычных клонах, так и на турбированных.

Проект для CPLD написан на Verilog в среде Quartus2, но может быть адаптирован под любые CPLD других производителей с достаточным количеством макроячеек.
Реализация PS/2 автомата не моя, её я позаимствовал из другого проекта, который был в свободном доступе и отлично работает в моём устройстве (моя реализация к сожалению работала только на макете, а в реальном устройстве - отказалась). Матрица спектрумовской клавиатыры и её обработчики мои.

На данный момент проект занимает 206 макроячеек (86% для данной CPLD), так что остаётся ещё немного свободных макроячеек для реализации какой-нибудь логиги на основной плате, благо свободных ножек у 100 выводного корпуса ещё очень много (некоьорые незадействованные IO на плате выведены на контактные площадки для пайки). Также в проекте есть несколько макросов, с помощью которых можно отключить некоторые функции (джойстик и комбинации кравиш) и сэкономить ещё пару десятков макроячеек.

Работа адаптера проверена на моём Ленинград 1, работает вполне стабильно.
Кроме стандартных 40 спектрумовских клавиш, добавлена поддержка комбинаций клавиш каких как, например, ковычки, точка, запятая, минус, равно, стрелки управления курсором, backspace. Функции Кемпстон джойстика назначены на цифровые клавиши (стрелки на 2,4,6,8б огонь - на Enter на нампаде). Любые клавиши можно легко переназначить в проекте.

Печатная плата устройства со всеми исправлениями находится в папке hardware/pcb. Расположение разъёмов срисовано с оригинальной платы Ленинград 1, поэтому долхно подойти на штатный разъём.



