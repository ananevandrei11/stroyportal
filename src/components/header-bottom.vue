<template>
  <section id="subHeader" class="subheader flex-center">
    <div class="wrapper flex-center">
      <figure class="subheader-logo">
          <img :src="imgLogo" alt="LOGO" class="img" />
      </figure>
      <button
        class="subheader-btn subheader-btn__catalog flex-center"
        id="btnCatalog"
      >
        <span><img :src="imgBurger" class="img" /></span>
        Каталог
      </button>
      <form class="subheader-search" name="searchHeader">
        <input
          type="text"
          name="search"
          id="search"
          placeholder="Хочу найти..."
          v-model="itemSearch"
          @input="autocomplite()"
        />
        <label for="search" @click="changeLocation()"><img :src="imgSearch" class="img" /></label>
        <div class="autocomplite" id="autocomplite">
          <ul>
            <li v-for="item in materials" :key="item.index" @click="setVal()">
              {{ item.name }}
            </li>
          </ul>
          <p id="lastItemSearch"></p>
        </div>
      </form>

      <button
        class="subheader-btn subheader-btn__list flex-center"
        id="btnList"
      >
        <span><img :src="imgList" class="img" /></span>
        Список
      </button>
      <button
        class="subheader-btn subheader-btn__accaunt flex-center"
        id="btnAccaunt"
      >
        {{ nameAccaunt }}
      </button>
    </div>
  </section>
</template>

<script>
import logo from '../assets/images/logo.svg';
import burger from '../assets/images/burger.svg';
import search from '../assets/images/search.svg';
import list from '../assets/images/list.svg';

export default {
  name: 'subHeader',
  data: () => {
    return {
      itemSearch: '',
      imgLogo: logo,
      imgBurger: burger,
      imgSearch: search,
      imgList: list,
      nameAccaunt: 'А',
      materials: [
        { name: 'Кермическая плитка' },
        { name: 'Сухие смеси' },
        { name: 'Пиломатериалы' },
        { name: 'Лако-красочные изделия' },
        { name: 'Наполные покрытия' },
        { name: 'Скобянные изделия' },
        { name: 'Сантехника' },
        { name: 'Садовая мебель' },
        { name: 'Электрика' },
        { name: 'Декор' },
      ],
    };
  },
  methods: {
    autocomplite: function () {
      function lightString(str, pos, len) {
        return (
          str.slice(0, pos) +
          '<mark>' +
          str.slice(pos, pos + len) +
          '</mark>' +
          str.slice(pos + len)
        );
      }
      function deleteVlock(elem) {
        elem.classList.add('close');
        elem.classList.remove('open');
        elem.innerHTML = elem.innerText;
      }
      function showBlock(elem) {
        elem.classList.remove('close');
        elem.classList.add('open');
      }

      let autocompBlock = document.getElementById('autocomplite');
      let lastItemSearch = document.getElementById('lastItemSearch');
      let val = this.itemSearch.toLowerCase().trim();
      let autocompBlockItem = autocompBlock.querySelectorAll(
        '#autocomplite ul li'
      );

      if (val != '') {
        autocompBlock.classList.add('open');
        lastItemSearch.innerText = 'Ничего не найдено';

        autocompBlockItem.forEach(function (elem) {
          if (elem.innerText.toLowerCase().search(val) == -1) {
            deleteVlock(elem);
          } else {
            showBlock(elem);
            lastItemSearch.innerText = '';
            let str = elem.innerText;
            elem.innerHTML = lightString(
              str,
              elem.innerText.toLowerCase().search(val),
              val.length
            );
          }
        });
      } else {
        autocompBlock.classList.remove('open');
        lastItemSearch.innerText = 'Ничего не найдено';
        autocompBlockItem.forEach(function (elem) {
          deleteVlock(elem);
        });
      }
    },
    setVal: function () {
      this.itemSearch = event.target.innerText;
      let autocompBlock = document.getElementById('autocomplite');
      autocompBlock.classList.remove('open');
    }
  },
};
</script>
