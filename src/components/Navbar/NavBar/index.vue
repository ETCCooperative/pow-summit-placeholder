<template>
  
  <nav
  class="z-40 sticky pl-8 pr-6 xl:px-28 py-navMobile md:py-8 text-headingsColor top-0 bg-background w-fullWidth border-b-2 lg:border-b-0 border-footerBorder"
  ref="navBar">
    <div class="flex items-center justify-between">
      <div class="w-logoMobileWidth cursor-pointer md:w-logoDesktopWidth h-logoDesktopheight flex float-left">
        <img src="pickaxe.png"/>
        <a href="#">
          <p class="text-sm w-full my-auto pl-3 text-headingsColor lg:text-2xl font-semibold font-notoSans">
            {{ $t("pow-summit.logo-title") }}
          </p>
        </a>
      </div>

      <!-- Shortcuts in the header-->
      <div class="items-end float-right lg:space-x-4 xl:space-x-8 flex text-lg">
        <a href="#overview"
          class="hidden lg:block font-roboto font-semibold text-textColor text-lg my-auto navItems hover:text-headingsColor transition duration-700">
          {{ $t("overview.nav-heading") }}
        </a>
        <a href="#venues"
          class="hidden lg:block font-roboto font-semibold text-textColor text-lg my-auto navItems hover:text-headingsColor transition duration-700">
          {{ $t("venues.nav-heading") }}
        </a>
        <a href="#ticketing"
          class="hidden lg:block font-roboto font-semibold text-textColor text-lg my-auto navItems hover:text-headingsColor transition duration-700">
          {{ $t("ticketing.nav-heading") }}
        </a>
        <a href="#monerokon"
          class="hidden lg:block font-roboto font-semibold text-textColor text-lg my-auto navItems hover:text-headingsColor transition duration-700">
          {{ $t("monerokon.nav-heading") }}
        </a>
        <a href="#prague"
          class="hidden lg:block font-roboto font-semibold text-textColor text-lg my-auto navItems hover:text-headingsColor transition duration-700">
          {{ $t("prague.nav-heading") }}
        </a>
        <a :href="$t('pow-summit.contact-us-link')"
          class="relative hidden lg:block font-notoSans font-semibold px-5 py-2 rounded text-headingsColor border-2 text-lg topApplyNow bg-gradient-to-r from-[#133706] to-[#53EB45]">
          {{ $t("pow-summit.contact-us-text") }} 
        </a>

        <!-- English/Chinese toggle-->
        <div class="my-auto text-black">
          <LocaleSwitcher />
        </div>

        <!-- This is not visible ? -->
        <img src="@/images/search.svg" class="my-auto lg:hidden ml-6" ref="navSearch" />

        <!-- Mobile-only hamburger view -->
        <img src="@/images/hamBurger.svg" v-on:click="openNav()" class="my-auto lg:hidden ml-6" id="menuIcon"
          ref="navOpen" />
      </div>
    </div>
  </nav>

  <div
  class="z-50 flex flex-col hidden lg:hidden pl-8 pr-6 pb-bodyY pt-3 max-h-screen bg-background w-screen top-6 fixed overflow-y-scroll"
  ref="navigation">
    <div class="">
      <img src="@/images/Cross.svg" v-on:click="closeNav()" class="ml-auto" id="menuIcon" ref="navClose" />
    </div>

    <!-- Mobile navigation -->
    <a :href="$t('pow-summit.contact-us-link')"
      class="py-1 mt-11 text-black text-center bg-gradient-to-r from-[#133706] to-[#53EB45] font-notoSans text-base font-bold rounded">
      <span class="text-headingsColor applyNowBtn relative">
        {{ $t("pow-summit.contact-us-text") }}
      </span>
    </a>

    <div v-for="(section, sectionKey) in sections" :key="sectionKey" :class="{'pt-6' : sectionKey > 0}">
      <a
        v-on:click="closeNav()"
        class="pt-6 font-notoSans text-headingsColor text-2xl font-bold leading-rightHeadingsDt"
        :href="section.target"
      >
        {{ $t(`sections.${section.key}`) }}
      </a>
      
      <div v-if="section.subsections">
        <div v-for="(subsection, subsectionKey) in section.subsections" :key="subsectionKey">
          <a
            v-on:click="closeNav()"
            :href="subsection.target"
          >
            <p class="font-notoSans text-textColor text-base font-normal pb-4">
              {{ $t(`subsection.${subsection.key}`) }}
            </p>
          </a>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
  import LocaleSwitcher from "@/components/LocaleSwitcher";
  import sections from "@/sections.json"

  export default {
    name: 'NavBar',
    components: {
      LocaleSwitcher
    },
    data(){
      return {
        sections: sections.data
      }
    },
    methods: {
      openNav() {
        this.$refs.navigation.classList.remove("hidden");
      },
      closeNav() {
        this.$refs.navigation.classList.add("hidden");
      }
    }
  }
</script>