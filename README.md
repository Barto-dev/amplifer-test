### Вопрос 1
Проведите код-ревью вот такого кода:
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Сто голов - сто умов</title>
  </head>
  <body>
    <header class="header">Жара в шапку не нагребешь</header>
    <main>
      <div class="nav" style="background: red;">
        <a class="link" href="#">Поди туда, не знаю куда</a> // TODO: define href
        <div class="button" role="button">Принеси то, не знаю что</div>
      </div>
      <article>
        <p class="paragraph-1">We couldn't delete some posts.<br />
          Please contact so-called «Support Master».</p>
        <p>&nbsp;</p>
        <p class="paragraph-2">
          <img src="confused.png" border="0" />
        </p>
        <p>Введите имя (от 4 до 8 символов). Это очень важно!</p>
        <input class="name-input" type="text" />
      </article>
    </main>
    <footer class="footer">Вы действительно уверены, что пол не может также быть потолком?</footer>
  </body>
</html>
```
```css
.header {
  font-family: Helvetica;
  font-size: 18px;
}

.nav {
  font-size: 14px;
}

.paragraph-1 {
  font-style: italic;
  color: #e7e7e7;
  margin: 5px;
  padding: 20px;
}

.paragraph-2 {
  font-style: italic;
  color: #e7e7e7;
  margin: 5px;
  padding: 20px;
}

.name-input:focus {
  outline: none;
}
```
---
Разбор первого задания сделал на кодпене, чтоб удобнее было смотреть 
https://codepen.io/Barto_i/pen/NWjqveQ

### Вопрос 2
Скажем, вы работаете над большим Реакт-компонентом. Пропсов довольно много и они все разнообразные по типу — строки, коллбеки, объекты и массивы. Вам бы хотелось оптимизировать количество апдейтов. Какой бы код вы написали внутри shouldComponentUpdate?

---

Взял бы вот эту утилиту например https://github.com/dashed/shallowequal
```js
 shouldComponentUpdate(nextProps, nextState) {
    const { props, state } = this;
    return !shallowequal(props, nextProps)
           && !shallowequal(state, nextState);
  }
```
### Вопрос 3
Представьте, что вам нужно сделать небольшой калькулятор. Например: https://journal.tinkoff.ru/halturka/. Какими технологиями вы бы воспользовались, какой бы выбрали фреймворк и как организовали бы код?

---
Взял бы какую то легковесную библиотеку с реактивностью, наверное это был бы Preact и для управления стейтом взял бы redux-zero. Он маленький (всего 473байта) и не имеет внешних зависимостей. Блоки с подсчетом разбил бы на отдельные компоненты и данные вычислений с этих блоков хранил в центральном сторе. Если упростить то для конкретно этого калькулятора очень хорошо зайдет flux архитектура.
### Вопрос 4
Как бы вы организовали данные, которые требуются для создания вот такой игры: https://arzamas.academy/mag/710-beatlesplus?

---
На эту игру хорошо ложится модель детерминированого конечного автомата. Где точка входа у нас всегда Beatles а точка выхода Монеточка ну и игра в каждый момент времени находится в каком то одном состоянии.  
Взял бы эту библиотечку https://github.com/davidkpiano/xstate и реализовал бы игру по такой вот схемке для этой игры и рендерил бы соответствующее состояние. 
Не реализовывал все возможные состояния так как это было бы долго:)

<div>
    <img align="center" src="https://raw.githubusercontent.com/Barto-dev/formurai/master/assets/logo.svg" alt="Logo" />
</div>

### Вопрос 5
Допустим, дизайнер предлагает вам внедрить в проект вариативный шрифт вместо Гельветики. Файл font.ttf весит 800 Кб. Что будете делать?

---
 Первым делом я бы посмотрел позволяет ли наша целевая аудитория использовать вариативный шрифт, так как в лисичке он до сих пор работает только на macOS https://caniuse.com/variable-fonts. 
И параллельным шагом нужно было бы оценить насколько позволительно это для проекта, если с большим к-ством посещений в день то гонять даже 50кб по сети может быть роскошью (страница поисковой выдачи яндекса по дефолту использует шрифт ариал например из этих же соображений). Если предыдущие 2 шага позволяют внедрить вариативный шрифт и 
это действительно нужно для уникальности и дизайна проекта то с помощью https://www.npmjs.com/package/glyphhanger извлёк бы подмножество нужных начертаний в формате woff2 другие не имеет 
смысла использовать так как браузеры которые умеют в вариативные шрифт уже давно умеют в woff2. После этих оптимизаций он весил бы 50kb~. И начали бы внедрять.
<div>
    <img align="center" src="https://raw.githubusercontent.com/Barto-dev/formurai/master/assets/logo.svg" alt="Logo" />
</div>
