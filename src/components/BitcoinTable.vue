
<template>
    <div class="table">
        <div class="table-header">
            <p><b>Date</b></p>
            <p><b>High</b></p>
            <p><b>Low</b></p>
            <p><b>Close</b></p>
        </div>
        <hr/>
        <div v-for="item in displayedItems" :key="item.time" class="table-item">
            <p class="item-date">{{ new Date(item.time * 1000).toLocaleDateString() }}</p>
            <p class="item-high">{{ item.high }}</p>
            <p class="item-low">{{ item.low }}</p>
            <p class="item-close">{{ item.close }}</p>
        </div>
        <div class="pagination">
            <button class="pagination-btn-lastnext" v-if="currentPage > 1" @click="currentPage--">Forrige</button>
            <button class="pagination-btn" v-for="page in pages" :key="page" @click="currentPage = page">{{ page }}</button>
            <button class="pagination-btn-lastnext" v-if="currentPage < pages.length" @click="currentPage++">Neste</button>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            listItem: [],
            currentPage: 1
        }
    },
    methods: {
        getListItems(){
        fetch('https://min-api.cryptocompare.com/data/v2/histoday?fsym=BTC&tsym=USD&limit=100&api_key=8ae55d463e1bf8d38b4a502ca47512f9b1dec21533ad9af7acb993e8ba952bc2')
            .then(response => response.json())
            .then(data => {
                this.listItem = data.Data.Data.reverse()
            })
        }
    },
    computed: {
        displayedItems() {
            const startIndex = (this.currentPage - 1) * 20;
            const endIndex = startIndex + 20;
            return this.listItem.slice(startIndex, endIndex);
        },
        pages() {
            const numberOfItems = this.listItem.length;
            const itemsPerPage = 20;
            const numberOfPages = Math.ceil(numberOfItems / itemsPerPage);
            return Array.from({ length: numberOfPages }, (current, i) => i + 1);
        }
    },
    mounted(){
        this.getListItems()
    }
}
</script>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
    @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@900&display=swap');

    .table {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        margin-left: 10%;
        margin-right: 10%;
        border-radius: 10px;
        padding: 8%;
        font-family: 'Roboto', sans-serif;
        color: #ffffff;
        background-image: url('../assets/mesh-52.png');
        background-size: cover;
        margin-bottom: 100px;
    }

    .table-header {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        margin-bottom: 2%;
        text-align: center;
        font-size: 1.3em;
        padding-left: 10%;
        padding-right: 10%;
    }

    .table-item {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        text-align: center;
        font-size: 1em;
        background-color: #27003380;
        margin-top: 2%;
        margin-bottom: 2%;
        padding: 2%;
        padding-left: 10%;
        padding-right: 10%;
        border-radius: 50px;
        transition: 0.5s;
    }

    .table-item:hover {
        background-color: #270033;
    }

    hr {
        width: 100%;
        border: 1px solid #270033;
    }

    .item-high {
        color: #00BFA5;
    }

    .item-low {
        color: #F44336;
    }

    .pagination {
        display: flex;
        flex-direction: row;
        justify-content: center;
        margin-top: 10%;
    }

    .pagination-btn {
        color: #ffffff;
        font-size: 1em;
        border: 2px solid #b10eb7;
        background-color: transparent;
        border-radius: 100px;
        padding: 1%;
        height: 50px;
        min-width: 50px;
        width: auto;
        margin: 1%;
        font-family: 'Roboto', sans-serif;
        cursor: pointer;
        transition: 0.5s;
    }

    .pagination-btn-lastnext {
        color: #ffffff;
        font-size: 1em;
        border: 2px solid #b10eb7;
        background-color: transparent;
        border-radius: 100px;
        padding: 1%;
        height: 50px;
        min-width: 80px;
        width: auto;
        margin: 1%;
        font-family: 'Roboto', sans-serif;
        cursor: pointer;
        transition: 0.5s;
        text-align: center;
        
    }

    .pagination-btn:hover, .pagination-btn-lastnext:hover {
        background-color: #b10eb7;
    }

    @media screen and (max-width: 768px) {
        .table-header {
            font-size: 1em;
        }

        .table-item {
            font-size: 0.8em;
        }

        .pagination-btn {
            font-size: 0.8em;
            height: 40px;
            min-width: 40px;
            width: auto;
        }
        .pagination-btn-lastnext {
            font-size: 0.8em;
            height: 40px;
            min-width: 60px;
            width: auto;
        }
    }

    @media screen and (max-width: 540px) {
        .table-header {
            font-size: 0.8em;
        }

        .table-item {
            font-size: 0.6em;
        }

        .pagination-btn {
            font-size: 0.6em;
            height: 30px;
            min-width: 30px;
            width: auto;
        }
        .pagination-btn-lastnext {
            font-size: 0.6em;
            height: 30px;
            min-width: 50px;
            width: auto;
        }
    }
</style>