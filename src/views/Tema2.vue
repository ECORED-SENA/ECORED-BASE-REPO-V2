<template lang="pug">
  .curso-main-container.pb-3
    BannerInterno
    .container.tarjeta.tarjeta--blanca.p-4.p-md-5.mb-5
      .titulo-principal.color-acento-contenido
        .titulo-principal__numero
          span 2
        h1 Titulo de primer nivel

</template>

<script>
export default {
  name: 'Tema2',
  data: () => ({
    // variables de vue
  }),
  watch: {
    // Escucha el cambio de sección desde el menú lateral
    '$route.hash'() {
      this.scrollToElement()
    },
  },
  mounted() {
    this.scrollToElement()
  },
  updated() {
    this.$aosRefresh()
  },
  methods: {
    scrollToElement() {
      this.$nextTick(() => {
        this.$aosRefresh()
        // 500ms da tiempo suficiente a que la animación de cierre del menú lateral
        // termine y libere el ancho/alto real del contenedor
        setTimeout(() => {
          const hash = this.$route.hash || window.location.hash
          if (!hash) return
          const element = document.querySelector(hash)
          if (element) {
            // Altura de la barra superior fija del SENA
            const headerOffset = 100
            const elementPosition = element.getBoundingClientRect().top
            const offsetPosition =
              elementPosition + window.pageYOffset - headerOffset
            window.scrollTo({
              top: offsetPosition,
              behavior: 'smooth',
            })
          }
        }, 500)
      })
    },
  },
}
</script>

<style lang="sass"></style>
