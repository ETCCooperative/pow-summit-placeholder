<template>
    <section>
      <div class="pt-6"></div>
      <div id="md-content" v-html="md(content)"></div>
    </section>
  </template>
  <script>
  export default {
    name: "Ticketing",
    watch: {
      "$i18n.locale": function (newLang) {
        this.getContent(newLang);
      },
    },
    data() {
      return {
        content: "",
      };
    },
    methods: {
      getContent(lang) {
        switch (lang) {
          case "en":
            import("@/md/ticketing.en.md").then((contentEN) => {
              this.content = contentEN.default;
            });
            break;
          case "cn":
            import("@/md/ticketing.cn.md").then((contentCH) => {
              this.content = contentCH.default;
            });
            break;
        }
      },
    },
    created() {
      const lang = this.$i18n.locale;
      this.getContent(lang);
    },
  };
  </script>
  