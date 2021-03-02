<template>
    <div class="progresso">
        <div class="barra-progresso">
            <div class="percentual">{{ progresso }}%</div>
            <div class="barra" :style="{width: progresso + '%'}"></div>
        </div>
    </div>
</template>

<script>
export default {
    props:{
        progresso: {type: Number, default: 0}
    }
}
</script>

<style>
.progresso{
    width: 600px;
    margin-bottom: 30px;
}

.barra-progresso{
    width: 100%;
    border: 1px solid #fff;
    color: #FFF;
    height: 35px;
    display: flex;
    align-items: center;
    position: relative;
}

.barra-progresso .percentual{
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
}

.barra-progresso .barra{
    background: chocolate;
    height: 100%;
    left: 0;
}
</style>