<template>
  <Dropdown placement="bottom-end">
    <DropdownTrigger
        :show-arrow="false"
        class="border text-left appearance-none cursor-pointer rounded text-sm font-bold ring-primary-200 dark:ring-gray-600 relative  inline-flex items-center justify-center bg-transparent border-transparent text-gray-500 dark:text-gray-400 hover:[&:not(:disabled)]:text-primary-500 h-9 min-w-9"
    >

      <Icon type="language" class="inline inline-flex items-center justify-center"  />
      <span class="ml-1 font-bold hidden md:inline mr-1" v-if="displayLanguageName == true">{{selectedDisplay}}</span>
    </DropdownTrigger>
    <template #menu>
      <DropdownMenu class=" py-1 px-1">
        <template v-for="(value,key) in langs">
            <DropdownMenuItem         
                               as="button"
                               class="flex items-center gap-2 block w-full text-left px-3 focus:outline-none rounded truncate whitespace-nowrap text-sm py-1.5 hover:bg-gray-50 dark:hover:bg-gray-800 focus:ring cursor-pointer text-gray-500 active:text-gray-600 dark:text-gray-500 dark:hover:text-gray-400 dark:active:text-gray-600 flex items-center gap-2"
                               @click.prevent="changeLang(key)"
            >
              <span  class="ml-2" v-if="selected!==key">{{value}}</span>
              <span class="ml-2 font-bold text-primary-500"  v-else>{{value}}</span>
            </DropdownMenuItem>
         
        </template>

      </DropdownMenu>
    </template>
  </Dropdown>

</template>

<script>

export default {
  name: "LanguageSwitcher",

  methods:{
    changeLang(key) {
      if (key !== this.selected) {
        Nova.request().get('/nova-vendor/language-switch/change/'+ key).then(() => {
          window.location.reload();
        });
      }
    },
  }

}
</script>
