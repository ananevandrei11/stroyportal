<template>
  <nav id="headerNavTop" class="nav flex-center">
    <div class="wrapper flex-center">
      <ul class="nav-list nav-list__location flex-center">
        <li class="nav-item nav-item__select flex-center">
          <span></span>
          Волгоградская область
        </li>
      </ul>
      <ul class="nav-list nav-list__other flex-center">
        <li class="nav-item" v-for="link in links" :key="link.index">
          <a href="" class="nav-link">
            {{ link.name }}
          </a>
        </li>
        <li class="nav-item nav-item__select flex-center">
          Другие сервисы
          <span></span>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: "headerNavTop",
  data: () => {
    return {
      links: [{ name: "Тендеры" }, { name: "База подрядчиков" }],
    };
  },
};
</script>