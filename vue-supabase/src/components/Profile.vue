<template>
    <form class="form-widget" @submit.prevent="updateProfile">
    <div>
        <label for="email">Email</label>
        <input id="email" type="text" :value="store.user.email" disabled  />
    </div>
    <div>
        <label for="username">Name</label>
        <input id="username" type="text" v-model="username" />
    </div>
    <div>
        <label for="website">Website</label>
        <input id="website" type="website" v-model="website" />
    </div>

    <div>
        <input
        type="submit"
        class="button block primary"
        :value="loading ? 'Loading...' : 'Update'"
        :disabled="loading"
        />
    </div>

    <div>
        <button class="button block" @click="signOut" :disabled="loading">
            Sign Out
        </button>
    </div>
    </form>
</template>

<script>
import { supabase } from "../supabase";
import { store } from "../store";
import { onMounted, ref } from "vue"; 

export default {
    setup() {
        const loading = ref(true)
        const userName = ref("")
        const website = ref("")
        const avatar_url = ref("")

        async function getProfile() {
            try {
                loading.value = true;
                store.user = supabase.auth.user();

                let { data, error, status } = await supabase
                .from("profiles")
                .select('username, website, avatar_url')
            }
        }
    }
}
</script>