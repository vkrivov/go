<h1>Скрипт для работы с SonarQube и локальным репозиторием Git</h1>

<h2>Проект реализует следующий функционал</h2>

Имеется список объектов конфигурации (файл список <i>объектов.ini</i>). Данный список разработчик составляет вручную в соответствии с выполняемыми задачами. Список задаётся в текстовом формате в наглядной форме. Пример списка:

Каталог: Тестовая база УТ<br>
Строка соединения: File="C:\Dev\UT"; Usr="Admin"; Pwd="Admin"<br>
{<br>
ОбщийМодуль.CRMЛокализация<br>
Документ.АвансовыйОтчет<br>
Документ.АвансовыйОтчет.Форма.ФормаДокумента<br>
Справочник.Номенклатура<br>
Справочник.Номенклатура.Форма.ФормаСписка<br>
C:\Разработка\Печать реестра.epf<br>
}

Далее вручную или по расписанию запускается скрипт (<i>go.os</i>). Скрипт на основании списка формирует командную строку пакетного режима запуска конфигуратора с нужными параметрами. Конфигуратор выгружает объекты из списка в файлы. Для этих файлов делается <i>git</i> <i>add</i> и <i>commit</i> и запускается <i>sonar-scanner</i>.

Цель проекта – возможность выполнить быструю проверку качества кода перед тем, как помещать доработки в рабочее хранилище. В этой связи используется только локальный репозиторий, push в публичный репозиторий не делается.

Скрипт выгружает в Git <b>все файлы</b>, а не только тексты модулей. Данное решение принято осознано. Git позволяет увидеть изменения только в текстовых файлах. Изменения, сделанные с помощью визуального конструктора, git не показывает. Вместе с тем, анализ xml файла формы зачастую позволяет получить об этом хотя бы общее представление. К примеру, достаточно легко можно понять, что после вот этого коммита на форме появилась вот эта кнопка.

С другой стороны, для анализа кода в каталог сканера выгружаются <b>только тексты модулей</b>.

Прочие файлы:<br> 
<i>init.os</i> – подготовка структуры каталогов и создание локального репозитория.<br>
<i>настройки.ini</i> – настройки, связанные с системой (пути к программам, токен Sonar и тому подобное)

<h2>Установка</h2>
Распаковать файлы в нужный каталог. Название и расположение каталога произвольные. После этого выполнить этом каталоге команду <i><b>oscript init.os</b></i> (данный скрипт нужно выполнить только один раз, при установке).

<h2>Настройка</h2>
Отредактировать файл <i>настройки.ini</i> в соответствии с настройками системы.<br>
Отредактировать файл <i>список объектов.ini</i> в соответствии с текущими задачами.

<h2>Выполнение</h2>
Выполнить команду<br> 
<i><b>oscript go.os "...Комментарий к коммиту..."</b></i><br>
либо, если комментарий не нужен, то <br>
<i><b>oscript go.os -nc</b></i>

<h2>Требования</h2>
Скрипт написан на OneScript, https://github.com/EvilBeaver/OneScript, предполагается, что в системе установлены и настроены:<br>
<b>OneScript</b>, https://oscript.io/<br>
<b>Git</b>, https://git-scm.com/<br>
<b>Sonarqube</b> и <b>Sonar-scanner</b>, https://www.sonarsource.com/<br>.
