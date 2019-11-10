<template>
    <div>
        <nav class="navbar navbar-expand-lg navbar-dark bg-dark">

            <div class="collapse navbar-collapse" id="navbar1">
                <ul class="navbar-nav mr-auto">
                    <li>
                        <a class="nav-link" @click="historyNav">История оплаченных счетов</a>
                    </li>
                    <li>
                        <a class="nav-link" @click="payFormNav">Оплатить счёт</a>
                    </li>
                </ul>
            </div>
        </nav>
    </div>
</template>

<script>
    export default {
        name: "Navbar",

        methods: {
            historyNav() {
                this.$emit("historyList")
            },
            payFormNav() {
                this.$emit("payFormList")
            },
        }
    }
</script>

