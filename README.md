<h1>Скрипт для работы с SonarQube и локальным репозиторием Git</h1>

<h2>Проект реализует следующий функционал</h2>

Имеется список объектов конфигурации (файл список _объектов.ini_). Данный список разработчик составляет вручную в соответствии с выполняемыми задачами. Список задаётся в текстовом формате в наглядной форме. Пример списка:

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

Далее вручную или по расписанию запускается скрипт (_go.os_). Скрипт на основании списка формирует командную строку пакетного режима запуска конфигуратора с нужными параметрами. Конфигуратор выгружает объекты из списка в файлы. Для этих файлов делается _git_ _add_ и _commit_ и запускается _sonar-scanner_.

Цель проекта – возможность выполнить быструю проверку качества кода перед тем, как помещать доработки в рабочее хранилище. В этой связи используется только локальный репозиторий, push в публичный репозиторий не делается.

Скрипт выгружает в Git **все файлы**, а не только тексты модулей. Данное решение принято осознано. Git позволяет увидеть изменения только в текстовых файлах. Изменения, сделанные с помощью визуального конструктора, git не показывает. Вместе с тем, анализ xml файла формы зачастую позволяет получить об этом хотя бы общее представление. К примеру, достаточно легко можно понять, что после вот этого коммита на форме появилась вот эта кнопка.

С другой стороны, для анализа кода в каталог сканера выгружаются **только тексты модулей**.

Прочие файлы:<br> 
_init.os_ – подготовка структуры каталогов и создание локального репозитория.<br>
_настройки.ini_ – настройки, связанные с системой (пути к программам, токен Sonar и тому подобное)

Скрипт написан на OneScript, https://github.com/EvilBeaver/OneScript

Предполагается, что на компьютере установлены и настроены **OneScript**, **Git**, **Sonarqube** и **Sonar-scanner**.
