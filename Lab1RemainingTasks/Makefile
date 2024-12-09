CС=gcc
CFLAGS= -Wall -Wextra
CLIBS= -lm

SOURCES=main2.c main9.c main10.c# Тут вы перечислятете файлы с вашими лабами по 1 файлу на задание
TEST_TEMPLATES_DIR=../test_templates# Это директория с шаблонами тестов (если вы их разместите в той же директории что и лабы пишите ./)
EXECUTABLES=$(SOURCES:.c=.a)
BASH=bash


SUCCESS_CMD=$(BASH) $(TEST_TEMPLATES_DIR)/success_cmd
FAILED_CMD=$(BASH) $(TEST_TEMPLATES_DIR)/failed_cmd

SUCCESS_RFILE_CMD=$(BASH) $(TEST_TEMPLATES_DIR)/success_rfile_cmd

SUCCESS_OFILE=$(BASH) $(TEST_TEMPLATES_DIR)/success_ofile
FAILED_OFILE=$(BASH) $(TEST_TEMPLATES_DIR)/failed_ofile

SUCCESS_RFILE_OFILE=$(BASH) $(TEST_TEMPLATES_DIR)/success_rfile_ofile

SUCCESS_IFILE_OFILE=$(BASH) $(TEST_TEMPLATES_DIR)/success_ifile_ofile
SUCCESS_IFILE_RFILE_OFILE=$(BASH) $(TEST_TEMPLATES_DIR)/success_ifile_rfile_ofile
FAILED_IFILE_OFILE=$(BASH) $(TEST_TEMPLATES_DIR)/failed_ifile_ofile
FAILED_IFILE_RFILE_OFILE=$(BASH) $(TEST_TEMPLATES_DIR)/failed_ifile_rfile_ofile


.PHONY: all test clean

all: $(EXECUTABLES) # Чтобы собрать все лабы надо ввести команду make

%.a : %.c
	$(CC) $(CFLAGS) $< $(CLIBS) -o $@

clean: # Чтобы удалить все исполняемые файлы надо ввести команду make clean
	rm -r -f *.a


# Принцип формирования названия выполняемого теста:
#
# (SUCESS|FAILED)[_IFILE][_RFILE](CMD|OFILE)
#		 1			2		3		 4
#
# 1){ОБЯЗАТЕЛЬНЫЙ} В зависимости от предполагаемого окончания теста мы выбираем либо успешный вариант - SUCCESS, либо провальный - FAILED 
# 2){ОПЦИОНАЛЬНЫЙ} При необходимости ввода в консоль программы (использвуя scanf или аналоги) добавляется суффикс _IFILE
# 3){ОПЦИОНАЛЬНЫЙ} Если программа предполагает наличие выходного файла с данными добавляется суффикс _RFILE
# 4){ОБЯЗАТЕЛЬНЫЙ} В зависимости от того однострочный или многострочный вывод в консоль ожидается у программы выбираем окончание CMD - для однострочного вывода и OFILE для многострочного
#


# Все тесты разделены на категории по результату работы программы и формату ввода:
#
# В случае если ввод в программу только с помощью аругментов командной строки:
# 	В случае если вывод в консоль у программы однострочный:
# 		1) Успешный с выводом в консоль (вывод сравнивается со строкой) - $(SUCCESS_CMD)
# 		2) Провальный с выводом в консоль (вывод сравнивается со строкой) - $(FAILED_CMD)
# 		3) Успешный с выводом в консоль и в файл (вывод сравнивается со строкой, а выходной файл с подготовленным файлом) - $(SUCCESS_RFILE_CMD)
#	
# 	В случае если вывод в консоль у программы многострочный:
# 		1) Успешный с выводом в консоль (вывод сравнивается со строками из файла) - $(SUCCESS_OFILE)
# 		2) Провальный с выводом в консоль (вывод сравнивается со строками из файла) - $(FAILED_OFILE)
# 		3) Успешный с выводом в консоль и в выходной файл (вывод сравнивается со строками из файла, а выходной файл с подготовленным файлом) - $(SUCCESS_RFILE_OFILE)
#
# В случае если ввод в консоль программы осуществляется из подготовленного файла а вывод у программы многострочный:  
# 	1) Успешный с вводом из файла, выводом в консоль (вывод сравнивается со строками из файла) - $(SUCCESS_IFILE_OFILE)
# 	2) Успешный с водом из файла, выводом в консоль и выходной файл (вывод сравнивается со строками из файла, а выходной файл с подготовленным файлом) - $(SUCCESS_IFILE_RFILE_OFILE)
# 	3) Провальный с вводом из файла, выводом в консоль (вывод сравнивается со строками из файла) - $(FAILED_IFILE_OFILE)
#


# Использование тестов:
#
# 1) $(SUCCESS_CMD) "<вызов исполняемого файла с его аргументами>" "<ожидаемый в консоль вывод>"
# 2) $(FAILED_CMD) "<вызов исполняемого файла с его аргументами>" "<ожидаемый код возврата отличный от 0>" "<ожидаемый в консоль вывод>"
# 3) $(SUCCESS_RFILE_CMD) "<вызов исполняемого файла с его аргументами>" "<ожидаемый в консоль вывод>" "<выходной файл>" "<файл с которым должен совпадать выходной файл>"
#
# 1) $(SUCCESS_OFILE) "<вызов исполняемого файла с его аргументами>" "<файл с ожидаемым в консоль выводом>"
# 2) $(FAIED_OFILE) "<вызов исполняемого файла с его аргументами>" "<ожидаемый код возврата отличный от 0>" "<файл с ожидаемым в консоль выводом>"
# 3) $(SUCCESS_RFILE_OFILE) "<вызов исполняемого файла с его аргументами>" "<файл с ожидаемым в консоль выводом>" "<выходной файл>" "<файл с которым должен совпадать выходной файл>"
# 
# 1) $(SUCCESS_IFILE_OFILE) "<вызов исполняемого файла с его аргументами>" "<файл данными которые вводятся в консоль через stdin>" "<файл с ожидаемым в консоль выводом>" 
# 2) $(SUCCESS_IFILE_RFILE_OFILE) "<вызов исполняемого файла с его аргументами>" "<файл данными которые вводятся в консоль через stdin>" "<файл с ожидаемым в консоль выводом>" "<выходной файл>" "<файл с которым должен совпадать выходной файл>"
# 3) $(FAILED_IFILE_OFILE) "<вызов исполняемого файла с его аргументами>" "<ожидаемый код возврата отличный от 0>" "<файл данными которые вводятся в консоль через stdin>" "<файл с ожидаемым в консоль выводом>"



#
# Ниже приведены примеры тестов. В выводе после теста должна быть краткая информация о том что это был за тест. "TEST N PASSED" это не информативно и принято не будет.
# Символ @ необходимо писать для подавления лишнего вывода в консоль при выполнении make файла.
#  

test_task_2: test_command_args_2 test_output_success_2_1 test_wrong_input_2 test_output_success_2_2 test_wrong_input_2_1
	

test_command_args_2:
	@$(FAILED_CMD) "main2.a" -1 "No arguments given."
	@echo "TASK 2: TEST WITH NO ARGUMENTS PASSED"


test_output_success_2_1:
	@$(SUCCESS_OFILE) "main2.a 0.00001" "2_output_for_task_2.txt"
	@echo "TASK 2: TEST WITH INPUT 0.00001 PASSED"

test_wrong_input_2:
	@$(FAILED_OFILE) "main2.a 0.abc01" -1 "./1_output_for_task_2.txt"
	@echo "TASK 2: TEST WITH INPUT 0.abc01 PASSED"

test_output_success_2_2:
	@$(SUCCESS_OFILE) "main2.a 0.1" "./3_output_for_task_2.txt"
	@echo "TASK 2: TEST WITH INPUT 0.1 PASSED"

test_wrong_input_2_1:
	@$(FAILED_OFILE) "main2.a 0.0001 0.3" -1 "./4_output_for_task_2.txt"
	@echo "TASK 2: TEST WITH TOO MANY ARGUMENTS PASSED"


test_task_9: test_command_args_9 test_failed_task_9 test_failed_task_9_1


test_command_args_9:
	@$(FAILED_CMD) "main9.a" -1 "Wrong amount of arguments!"
	@echo "TASK 9: TEST WITH NO ARGUMENTS PASSED"

test_failed_task_9: 
	@$(FAILED_OFILE) "main9.a 100 -10" -1 "./1_output_for_task_9.txt"
	@echo "TASK 9: TEST WITH WRONG INPUT PASSED"

test_failed_task_9_1:
	@$(FAILED_OFILE) "main9.a -10 100 qwerty" -1 "./2_output_for_task_9.txt"
	@echo "TASK 9: TEST WITH WRONG AMOUNT OF ARGUMENTS PASSED"


test_task_10: test_command_args_10 test_success_task_10 test_success_task_10_1 test_failed_task_10


test_command_args_10:
	@$(FAILED_CMD) "main10.a" -1 "Wrong number of arguments!"
	@echo "TASK 10: TEST WITH NO ARGUMENS PASSED"

test_success_task_10:
	@$(SUCCESS_IFILE_OFILE) "main10.a 9" "1_input_for_task_10.txt" "1_output_for_task_10.txt" 
	@echo "TASK 10: TEST WITH RIGHT ARGUMENTS PASSED"

test_success_task_10_1:
	@$(SUCCESS_IFILE_OFILE) "main10.a 36" "2_input_for_task_10.txt" "2_output_for_task_10.txt"
	@echo "TASK 10: TEST WITH NOT NESSECARY 0 PASSED"

test_failed_task_10:
	@$(FAILED_OFILE) "main10.a 33 22" -1 "3_output_for_task_10.txt"
	@echo "TASK 10: TEST WITH TOO MANY ARGUMENTS PASSED"

test: test_task_2 test_task_9 test_task_10 # Здесь перечисляются все написанные вами тесты. Запуск тестов производится по команде make test
	