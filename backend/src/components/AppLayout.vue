<template>
    <div v-if="currentUser.id" class="min-h-full bg-gray-200 flex">
        
    </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';
import Sidebar from './Sidebar.vue';
import Navbar from './Navbar.vue';
import store from '../store';
import Spinner from './core/Spinner.vue';
import Toast from './core/Toast/vue';

const { title } = defineProps({
    title: String
});
const sidebarOpened = ref(true);
const currentUser = computed(() => store.state.user.data);

function toggleSidebar() {
    sidebarOpened.value = !sidebarOpened.value;
}

function updateSidebarState() {
    sidebarOpened.value = window.outerWidth > 768;
}

onMounted(() => {
    store.dispatch('getCurrentUser');
    store.dispatch('getCountries');
    updateSidebarState();
    window.addEventListener('resize', updateSidebarState)
});

onUnmounted(() => {
    window.removeEventListener('resize', updateSidebarState)
});

</script>
