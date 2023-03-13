

<template>
    <div class="header">
        <img src="../assets/bitcoin.png" alt="bitcoin" id="bitcoin-img">
        <h1 id="bitcoin-title">Daily Bitcoin Update</h1>
    </div>
</template>

<style>
    @import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
    @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@900&display=swap');

    .header {
        padding: 3%;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: center;
        font-family: 'Roboto', sans-serif;
        color: #ffffff;
    }

    #bitcoin-img {
        height: auto;
        max-height: 50px;
    }

    #bitcoin-title {
        font-size: 2em;
        margin-left: 1em;
    }

    @media (max-width: 768px) {
        #bitcoin-title {
            font-size: 1.5rem;
        }
        #bitcoin-img {
            max-height: 50px;
        }
    }
</style>