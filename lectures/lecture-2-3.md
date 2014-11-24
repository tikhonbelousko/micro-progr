# Лекция 2.3

## Режимы работы процессора архитектуры x86

Есть два режима работы:

- реальный;
- защищенный.

Начиная с процессоров 80286 вводится поддержка многозадачности и защищенной архитекрутры на аппаратном уровне.

В целях совместимости с младшими (8086/8088) данный процессор поддерживал два режима работы:

- реальный режим (режим реального адреса);
- защищенный режим (режим защещенной виртуальной адресации).

В реальном режиме процессор вел себя ровно как 8086. В режиме защищенном процессор использовал все возможности.

В момент включения компьютера процессор работает в режиме 8086, после загрузки ядра включается защищенный режим.

**В режиме эмуляции 8086:**

- загружаются программы BIOS;
- инициализация компонентов необходимых для защищенного режима.

*OS DOS* (одназадачная) - не переводит процессор в защищенный режим, т.к. она однозадачная. Это могут делать программы если им это нужно.

### Характерны особенности реального режима:

1. Возможна адресация до 1 Мб.

	**Формирование адреса**: *<номер сегмента>* * 16 + *<16 бит смещения>*
	
	**Пр.** 0400h:0001h = 400h * 16 + 0001
	
	8086 - 20-битная адресная шина 2^20 бит= 1 Мб
	80286 - 24-битная шина: 2^24 бит = 16 Мб
	
	В целях совместимости введен логический элемент Gate A20 - перекрывает 4 	последних бита.
	
	
2. Сегментная модель

	Размер сегмента не превышает 64кб. В сегментных регистрах DS, CS находится адрес сегмента.

3. Нет поддержки многозадачности - нет необходимости контролировать взаимное влияние программ.

4. Любая программа может обратиться к любому участку памяти.

### Характерны особенности защищенного режима:

Основная цель - поддержка многозадачности.

Задачи:

 - Исключить взаимное влияние программ;
 - Обеспечить корректное взаимодействие между программами.

Особенности:
 
1. Меняется принцип работы с памятью
2. Меняются функции и список программно-аппартных компонентовучавствующих в организации доступа к памяти.
3. Остается сегментная модель. Каждый сегмент памяти снобжаетс доп. характеристиками.
	1. Размер сегмента
	2. Набор атрибутов, достаточный для того, чтобы часть контроля над сегментом отдать аппартной части.
	
##### Принципы сегоментной организации памяти

![
](images/l2-3-1.jpg)
*рис. Принципы работы сегментов*

Сегмент соответсвует процессу. Процесс видит не все адресное пространство, а только область сегмента.

Раздачей сегментов занимается ядро ОС - реализует изоляцию процессов.



