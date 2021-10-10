<template>
    <div>
        <p>{{exibirMsg}}</p>
    </div>
    
</template>


<script>
export default {
    name: "Msg",
    props: {
        exibirMsg: String
    }
}
</script>


<style scoped>
    div {
        display: flex;
        justify-content: center;
        align-items: center;
    }

    p {
    /* border: solid; */
    height: 75px;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 10px;
    margin-bottom: 10px;
    font-size: 22px;
    color: white;
    background-color: #80c1d5;
    border-radius: 8px;
    border: solid 2px #78b4c7;

 /*    animation: changeColor 1s infinite; */

}


/* @keyframes changeColor {
        0% { background-color: var(--primary-color);}
        50% { background-color: var(--secundary-color);}
        75% { background-color: var(--primary-color);}
        100% { background-color: var(--primary-color);}
} */
</style>