<template>
  <nav>
    <div class="logo">
      <router-link to="/"><img :src="imgSrc" alt="logo" style="width: 150px;"></router-link>
    </div>
    <ul class="nav-links">
      <li v-for="(item, index) in navItems" :key="index">
        <router-link :to="item.path">{{ item.name }}</router-link>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      navItems: [
        { name: '作品', path: '/projects' },
        { name: '关于我', path: '/about' },
        { name: '联系我', path: '/contact' },
      ],
      imgSrc: require('../assets/img/logo1.png')
    }
  },
};
</script>

<style scoped>
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
  background-color: #222;
}

.logo {
  font-size: 1.5rem;
  font-weight: bold;
}

.nav-links {
  display: flex;
  list-style-type: none;
}

.nav-links li {
  margin-left: 1.5rem;
}

.nav-links a {
  color: #fff;
  text-decoration: none;
  transition: color 0.3s;
}

.nav-links a:hover {
  color: #ccc;
}
</style>
