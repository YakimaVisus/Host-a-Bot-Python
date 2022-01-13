# Хостим свой скрипт (у мя бот) на Heroku 
Логинимся через терминал/cmd  
heroku login  

#Создаём приложение с Python билдпаком  
cd %directory%  
heroku create %app_name% --buildpack http://github.com/heroku/heroku-buildpack-python.git  

cd %directory% — перемещение в директорию где расположен бот  
%app_name% — название вашего приложения  

# Настройка приложения  
Создаем необходимые файлы конфигурации:  

runtime.txt  
requirements.txt //уже есть в проекте бота  
Procfile //без расширения  

runtime.txt:  

python-2.7.13 or python-3.6.0 //выбрать одно, в нашем случае python-3.6.0  

requirements.txt:  

//указываем необходимые модули  
//каждый модуль с новой строки  

Procfile:  

web: %app_name%.py //исполняемый файл*, который будет получать входящий трафик от роутеров heroku worker: python %not_web_app%.py //исполняемый файл, которому не требуется входящий трафик для работы  

*Этими исполняемыми файлами являются: боты, работающие на основе вебхуков, веб серверы.  
Следует пояснить по поводу файла процессов (Procfile): в бесплатной версии мы можем создавать до двух процессов, по 1 на каждый тип.  

В нашем случае понадобится только:  

worker: python %not_web_app%.py // vbot.py  

# Загружаем бота через git  
Не забудьте убрать settings.py из .gitignore  

git init  
heroku git:remote -a %app_name%  
git add .  
git commit -am "make it better"  
git push heroku master  
