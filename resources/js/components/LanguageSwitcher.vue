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
      <DropdownMenu>
        <template v-for="(value,key) in langs">
          <div class="flex flex-col py-1">
            <DropdownMenuItem
                              :key="key"
                               as="button"
                               class="flex items-center hover:bg-gray-100"
                               @click.prevent="changeLang(key)"
            >
              <span  class="ml-2" v-if="selected!==key">{{value}}</span>
              <span class="ml-2 font-bold text-primary-500"  v-else>{{value}}</span>
            </DropdownMenuItem>
          </div>
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
