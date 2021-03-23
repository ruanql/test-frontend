<template>
    <main>
        <section>
            <div class="text-left py-3">
            <div class="container">
                <div class="row">
                <div class="col-md">
                    <h1>{{ info.name }}</h1>
                    <p>ID do cliente: {{ info.id }}</p>
                </div>
                </div>
            </div>
            </div>
        </section> 
    </main>
</template>

<script>
import api from "@/services/api.js";

export default {
    name: "Item",
    data() {
        return {
            info:[]
        }
    },
    mounted() {
        api.get("https://www.mocky.io/v2/5c7552e43100009c20c23450").then(response =>{
            this.info = response.data.customer;
        });
    }
}
</script>

<style scoped>

</style>