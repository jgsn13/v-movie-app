<template>
  <header>
    <router-link to="/">
      <h1><span>V</span>ovies</h1>
    </router-link>
  </header>
  <main>
    <router-view />
  </main>
</template>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;

  &::selection {
    background: transparentize(#8043e2, 0.5);
  }
}

body {
  background-color: #42355e;
}

a {
  text-decoration: none;
}

header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: #3b2c4e;
  box-shadow: 0px 0px 6px rgba(#000000, 0.1);

  h1 {
    color: #ffffff;
    font-size: 28px;

    span {
      color: #8043e2;
    }
  }
}
</style>
