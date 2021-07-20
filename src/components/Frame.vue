<template>
  <div class="h-screen flex overflow-hidden bg-gray-100 ">
    <TransitionRoot as="template" :show="sidebarOpen">
      <Dialog as="div" static class="fixed inset-0 flex z-40" @close="sidebarOpen = false" :open="sidebarOpen">
        <TransitionChild as="template" enter="transition-opacity ease-linear duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="transition-opacity ease-linear duration-300" leave-from="opacity-100" leave-to="opacity-0">
          <DialogOverlay class="fixed inset-0 bg-gray-600 bg-opacity-75" />
        </TransitionChild>
        <TransitionChild as="template" enter="transition ease-in-out duration-300 transform" enter-from="-translate-x-full" enter-to="translate-x-0" leave="transition ease-in-out duration-300 transform" leave-from="translate-x-0" leave-to="-translate-x-full">
          <div class="relative flex-1 flex flex-col max-w-xs w-full pt-5 pb-4 bg-indigo-700">
            <TransitionChild as="template" enter="ease-in-out duration-300" enter-from="opacity-0" enter-to="opacity-100" leave="ease-in-out duration-300" leave-from="opacity-100" leave-to="opacity-0">
              <div class="absolute top-0 right-0 -mr-12 pt-2">
                <button type="button" class="ml-1 flex items-center justify-center h-10 w-10 rounded-full focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white" @click="sidebarOpen = false">
                  <span class="sr-only">Close sidebar</span>
                  <XIcon class="h-6 w-6 text-white" aria-hidden="true" />
                </button>
              </div>
            </TransitionChild>
            <div class="flex items-center flex-shrink-0 px-4">
              <h1 class="text-white">Explore</h1>
            </div>
            <div class="mt-5 flex-grow flex flex-col">
              <nav class="flex-1 px-2 space-y-1 bg-white" aria-label="Sidebar">
                <template v-for="item in navigation" :key="item.name">
                  <div v-if="!item.children">
                    <a :href="item.href" :class="[item.current ? 'bg-gray-100 text-gray-900' : 'bg-white text-gray-600 hover:bg-gray-50 hover:text-gray-900', 'group w-full flex items-center pl-7 pr-2 py-2 text-sm font-medium rounded-md']">
                      {{ item.name }}
                    </a>
                  </div>
                  <Disclosure as="div" v-else class="space-y-1" v-slot="{ open }">
                    <DisclosureButton :class="[item.current ? 'bg-gray-100 text-gray-900' : 'bg-white text-gray-600 hover:bg-gray-50 hover:text-gray-900', 'group w-full flex items-center pr-2 py-2 text-left text-sm font-medium rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500']">
                      <component :is="item.icon" class="mr-3 flex-shrink-0 h-6 w-6 text-gray-400 group-hover:text-gray-500" aria-hidden="true" />
                        {{ item.name }}
                      <svg :class="[open ? 'text-gray-400 rotate-90' : 'text-gray-300', 'mr-2 flex-shrink-0 h-5 w-5 transform group-hover:text-gray-400 transition-colors ease-in-out duration-150']" viewBox="0 0 20 20" aria-hidden="true">
                        <path d="M6 6L14 10L6 14V6Z" fill="currentColor" />
                      </svg>
                    </DisclosureButton>
                    <DisclosurePanel class="space-y-1">
                      <a v-for="subItem in item.children" :key="subItem.name" :href="subItem.href" class="group w-full flex items-center pl-10 pr-2 py-2 text-sm font-medium text-gray-600 rounded-md hover:text-gray-900 hover:bg-gray-50">
                        {{ subItem.name }}
                      </a>
                    </DisclosurePanel>
                  </Disclosure>
                </template>
              </nav>
            </div>
          </div>
        </TransitionChild>
        <div class="flex-shrink-0 w-14" aria-hidden="true">
          <!-- Dummy element to force sidebar to shrink to fit close icon -->
        </div>
      </Dialog>
    </TransitionRoot>

    <!-- Static sidebar for desktop -->
    <div class="hidden bg-indigo-700 md:flex md:flex-shrink-0">
      <div class="flex flex-col w-64">
        <!-- Sidebar component, swap this element with another sidebar if you like -->
        
        <div class="flex flex-col flex-grow border-r border-gray-200 pt-5 pb-4 bg-indigo overflow-y-auto">
          <div class="flex items-center flex-shrink-0 px-4">
            <h1 class="text-white">Explore</h1>
          </div>
          <div class="mt-5 flex-grow flex flex-col">
            <nav class="flex-1 px-2 space-y-1 bg-white" aria-label="Sidebar">
              <template v-for="item in navigation" :key="item.name">
                <div v-if="!item.children">
                  <a :href="item.href" :class="[item.current ? 'bg-gray-100 text-gray-900' : 'bg-white text-gray-600 hover:bg-gray-50 hover:text-gray-900', 'group w-full flex items-center pl-7 pr-2 py-2 text-sm font-medium rounded-md']">
                    {{ item.name }}
                  </a>
                </div>
                <Disclosure as="div" v-else class="space-y-1" v-slot="{ open }">
                  <DisclosureButton :class="[item.current ? 'bg-gray-100 text-gray-900' : 'bg-white text-gray-600 hover:bg-gray-50 hover:text-gray-900', 'group w-full flex items-center pr-2 py-2 text-left text-sm font-medium rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500']">
                    <component :is="item.icon" class="mr-3 flex-shrink-0 h-6 w-6 text-gray-400 group-hover:text-gray-500" aria-hidden="true" />
                    {{ item.name }}
                    <svg :class="[open ? 'text-gray-400 rotate-90' : 'text-gray-300', 'mr-2 flex-shrink-0 h-5 w-5 transform group-hover:text-gray-400 transition-colors ease-in-out duration-150']" viewBox="0 0 20 20" aria-hidden="true">
                      <path d="M6 6L14 10L6 14V6Z" fill="currentColor" />
                    </svg>
                  </DisclosureButton>
                  <DisclosurePanel class="space-y-1">
                    <a v-for="subItem in item.children" :key="subItem.name" :href="subItem.href" class="group w-full flex items-center pl-10 pr-2 py-2 text-sm font-medium text-gray-600 rounded-md hover:text-gray-900 hover:bg-gray-50">
                      {{ subItem.name }}
                    </a>
                  </DisclosurePanel>
                </Disclosure>
              </template>
            </nav>
          </div>
        </div>
      </div>
    </div>
    <div class="flex flex-col w-0 flex-1 overflow-hidden">
      <div class="relative z-10 flex-shrink-0 flex h-16 bg-white shadow">
        <button type="button" class="px-4 border-r border-gray-200 text-gray-500 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500 md:hidden" @click="sidebarOpen = true">
          <span class="sr-only">Open sidebar</span>
          <MenuAlt2Icon class="h-6 w-6" aria-hidden="true" />
        </button>
        <div class="flex-1 px-4 flex justify-between">
          <div class="flex-1 flex">
          </div>
          <div class="ml-4 flex items-center md:ml-6">
            <button class="bg-white p-1 m-1 rounded-full text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
              <span class="sr-only">View notifications</span>
              <BellIcon class="h-6 w-6" aria-hidden="true" />
            </button>
            <button class="bg-white p-1 m-1 rounded-full text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
              <span class="sr-only">View Settings</span>
              <CogIcon class="h-6 w-6" aria-hidden="true" />
            </button>

            <!-- Profile dropdown -->
            <Menu as="div" class="ml-3 relative">
              <div>
                <MenuButton class="max-w-xs bg-white flex items-center text-sm rounded-full focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                  <span class="sr-only">Open user menu</span>
                  <span class="inline-flex items-center justify-center h-8 w-8 rounded-full bg-gray-500">
                    <span class="text-sm font-medium leading-none text-white">TW</span>
                  </span>
                </MenuButton>
              </div>
              <transition enter-active-class="transition ease-out duration-100" enter-from-class="transform opacity-0 scale-95" enter-to-class="transform opacity-100 scale-100" leave-active-class="transition ease-in duration-75" leave-from-class="transform opacity-100 scale-100" leave-to-class="transform opacity-0 scale-95">
                <MenuItems class="origin-top-right absolute right-0 mt-2 w-48 rounded-md shadow-lg py-1 bg-white ring-1 ring-black ring-opacity-5 focus:outline-none">
                  <h1>Account</h1>
                  <span class="inline-flex items-center justify-center h-8 w-8 rounded-full bg-gray-500">
                    <span class="text-sm font-medium leading-none text-white">TW</span>
                  </span>
                  <MenuItem v-for="item in userNavigation" :key="item.name" v-slot="{ active }" :is="item.icon">
                    <a :href="item.href" :class="[active ? 'bg-gray-100' : '', 'block px-4 py-2 text-sm text-gray-700']">{{ item.name }}</a>
                  </MenuItem>
                </MenuItems>
              </transition>
            </Menu>
          </div>
        </div>
      </div>

      <main class="flex-1 relative overflow-y-auto focus:outline-none">
        <div class="py-6">
          <div class="max-w-7xl mx-auto px-4 sm:px-6 md:px-8">
            <h1 class="text-2xl font-semibold text-gray-900">Explore Home Page</h1>
          </div>
          <div class="max-w-7xl mx-auto px-4 sm:px-6 md:px-8 flex flex-row">
            <!-- Replace with your content -->
            <div class="m-2 flex-grow">
              <div class="bg-white px-4 py-5 border-b border-gray-200 sm:px-6">
                <div class="-ml-4 -mt-2 flex items-center justify-between flex-wrap sm:flex-nowrap">
                  <div class="ml-4 mt-2">
                    <h3 class="text-lg leading-6 font-medium text-gray-900">
                      Bilingual Department Reporting
                    </h3>
                  </div>
                  <div class="ml-4 mt-2 flex-shrink-0">
                    <button type="button" class="relative inline-flex items-center px-4 py-2 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                      Progress Review
                    </button>
                  </div>
                </div>
              </div>            
            </div>
            <div class="p-4 m-2 flex-grow bg-white">
              <h1 class="font-bold">Profile</h1>
              <userProfile/>
            </div>
            <!-- /End replace -->
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
import {
  Dialog,
  DialogOverlay,
  Menu,
  MenuButton,
  MenuItem,
  MenuItems,
  TransitionChild,
  TransitionRoot,
  Disclosure,
  DisclosureButton,
  DisclosurePanel
} from '@headlessui/vue'
import {
  BellIcon,
  HashtagIcon,
  BookOpenIcon,
  //FolderIcon,
  HomeIcon,
  //InboxIcon,
  MenuAlt2Icon,
  //UsersIcon,
  XIcon,
  CogIcon,
} from '@heroicons/vue/outline'
//import { SearchIcon } from '@heroicons/vue/solid'
import userProfile from './UserProfile'

const navigation = [
  {
    name: 'Explore',
    icon: HomeIcon,
    current: true,
    children: [
      { name: 'Curriculum', href: '#' },
      { name: 'LION', href: '#' },
    ],
  },
  {
    name: 'LION Math',
    icon: HashtagIcon,
    current: false,
    children: [
      { name: 'Math Item 1', href: '#' },
      { name: 'Math Item 2', href: '#' },
    ],
  },
  {
    name: 'LION Reading',
    current: false,
    icon: BookOpenIcon,
    children: [
      { name: 'Reading Item 1', href: '#' },
      { name: 'Reading Item 2', href: '#' },
    ],
  },
]
const userNavigation = [
  { name: 'Your Profile', href: '#' },
  { name: 'Sign out', href: '#' },
]

export default {
  components: {
    Dialog,
    DialogOverlay,
    Menu,
    MenuButton,
    MenuItem,
    MenuItems,
    TransitionChild,
    TransitionRoot,
    BellIcon,
    MenuAlt2Icon,
    //SearchIcon,
    XIcon,
    CogIcon,
    userProfile,
    Disclosure,
    DisclosureButton,
    DisclosurePanel,
  },
  setup() {
    const sidebarOpen = ref(false)

    return {
      navigation,
      userNavigation,
      sidebarOpen,
    }
  },
}
</script>